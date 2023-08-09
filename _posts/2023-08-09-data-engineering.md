---
layout: post
title: Data engineering for RootTracker
author: Jesse Windle
---


One of the nice things about working at a young start up is that you
get to wear multiple hats.  For instance, at Hi Fidelity Genetics /
Technologies, my title was data scientist, but there were times where
I got to be a data engineer as well, which was a lot of fun!  Here I
will describe our data stack and offer a few lessons learned along the
way.


# Background

Hi Fidelity Genetics developed a root phenotyping device called
RootTracker.  The device has electrodes arrayed around a root crown in
a cylindrical fashion.  As seen in the image below, there were 12
vertical, printed circuit board (PCB) "paddles", each of which had 22
electrodes.  The device measured voltage at these electrodes for three
different charging parameters at regular intervals.  These voltages
were ultimately transformed into root detections --- that is the
device detected a root at a certain time in a certain place.  (You can
read more about the set up in our paper ["Capturing in-field root
system dynamics with
RootTracker"](https://academic.oup.com/plphys/article/187/3/1117/6328791).)

![](roottracker.jpg)

The devices used a radio to send data to a base station.  This data was
aggregated across several devices, which was then uploaded as a single
file to Amazon Web Services (AWS).  There are probably several ways
we could have improved our data management at the point of the base
station, but we will take the single file uploads from the base
station as our starting point for describing our data stack.  The
whole thing evolved in a rather organic way and what I describe below
mostly describes where we ended, as opposed to where we started.  I
will also make some modifications to avoid delving into historical or
technical details.


# Schema

Instead of giving a technical description of the schema, let me
describe the objects that were modeled, since that provides a better
overview.  As mentioned previously, we had `Device`s that measured
voltages.  Each paddle on a device sent a `Measurement` that reported
the device and paddle that the measurements came from, the charging
parameters, and 22 voltages, one for each sensor on a paddle.  A
`Trial` refers a specific experiment.  Each `Trial` was associated
with a set of device `Deployment`s, effectively linking a `Device`
with a `Trial` and recording some additional information in the
process, like the location of the `Device`.  Each `Device` possessed
firmware, which controlled how the device operated along with
statically set network information.  Because that firmware could
change, there were separate `Software` records that tracked the
firmware version and the configuration of the `Device`.  

In agricultural experiments, it is standard to have a "field book"
that tracks the `Treatment`s used across the field.  A `Treatment` was
always a categorical (potentially ordered) variable.

An algorithm processed the raw data to produce detections.  (The story
of the detection algorithm is quite interesting in and of itself.)
The first version of our `Detection`s recorded the time, paddle, and
electrode where it occurred.  Later, we realized that we also needed
to include quality control metrics to identify periods when the
detection algorithm might be unreliable.  That led to the a more
generic notion of `Feature`s, which were a time-indexed
multidimensional array
derived from the raw data.  


# API

Like our discussion of the schema above, we describe how to interact
with objects from the schema --- the API --- at a high level.

In some cases, the API was very transparent.  For instance, one could
get `Trial`s, `Device`s, `Deployment`s using a variety of filters.
Inserting those objects was (mostly) just a matter of populating their
fields.

In other cases, the API was doing a lot under the hood.  For instance,
our field scientist designed the experiments and kept track of additional
experiment data using a traditional field book, which we can think of
as a spreadsheet.  Each row of the field book was one experimental
unit, which were plants when conducting a RootTracker trial.  The
columns of the field book were effectively covariates --- treatments
or observations, like the variety, growth stage, location, or device
barcode of a plant.  One could send a row from a field book to the API
to update or insert the treatments.  However, the treatments were
recorded in a key-value fashion, so in actuality the API would be
updating or inserting several records in one go.  Conversely, when
exporting a field book, one would have to gather many records to
recapitulate a single row of the field book.

One could get `Measurement`s transparently by the device barcode,
time, and charging parameters, but we had a bespoke procedure for
inserting `Measurement`s since they came from a tarballed file of
aggregated measurements.  In that case it made more sense to process a
whole file together, instead of each measurement within a file
individually.


# Implementation

Based on our teams' experience, we used SQL for our database
([PostgreSQL](https://www.postgresql.org/) and
[SQLAlchemy](https://www.sqlalchemy.org/), specifically).  Eventually,
we also developed an alternative approach for storing the
`Measurement`s and `Feature`s --- using [Apache
Iceberg](https://iceberg.apache.org/) /
[Tabular](https://tabular.io/).

We employed the [OpenAPI](https://www.openapis.org/) framework to
specify our API.  We found the free [Swagger
editor](https://editor.swagger.io/) to be sufficient for our purposes.
We used [Flask](https://flask.palletsprojects.com/) to implement the
API.  While our system was only used internally, we did ultimately
develop the capability to control access to the API using Keycloak.

An aside... obviously, cost is an important factor when deciding how
to put together a system.  On AWS, it is more expensive to run an SQL
database than it is to retrieve data from S3 storage.  Why is that and
what is the difference?

When you run an Instance on AWS, it is like turning on a computer.
You have a CPU, RAM, and a hard drive.  The hard drive is the key for
our current discussion.  A hard drive has a file system.  You can
combine several hard drives using RAID to create a larger file system
with insurance against failure; however, there is a limit to how big
you can make the file system.  That becomes problematic if you are
doing something like crawling the web, as the
data collected is so copious.  

To overcome that problem, a new approach was developed with Apache
Hadoop being the canonical software.  Hadoop uses commodity hardware
to scale a file system to arbitrary size.  To do that the Hadoop file
system gives up some of the POSIX requirements that are found in a
typical file system.  Hadoop also allows one to compute statistics and
similar computations for a dataset on this file system, which is
nontrivial when you consider that it is a highly decentralized system.

In terms of how all this relates to options on AWS, the hard drive one
uses for an AWS Instance or for a persistent SQL database uses the old
school hard drive, whereas AWS S3 is effectively Hadoop (or a
successor of Hadoop).

Naturally, one still wants to organize data stored on something like
S3.  The original solution to that was Apache Hive.  Data is stored as
flat files, which possess some sort of schema.  Those files can be
indexed on a value that is constant within the file or on metadata
about fields of the file.  Data can be retrieved using an SQL-like
language.  Apache Iceberg is a successor to Hive that aims to solve
some of its shortcomings.  The bottom line is that one can store,
retrieve, and compute statistics for large amounts of structured data
using a more cost effective form of storage, which can also obviate
any worries about how large that data may grow.


# Conclusion

Looking back on this, the idea of design keeps wandering through my
mind.

If we think about architecture, like architecture of buildings, an
architect needs to know about the limitations of the materials used in
the design, but does not need to know how to do carpentry, masonry,
etc.  The architect provides the blueprint and then the subcontractors
do the work.  In some sense though, the building is done when the
blueprint is done.

Within the context of a system, you could make a similar split.  The
blueprint is the database schema and API documentation.  The
subcontractors are the people and software used to implement the API
and data storage.  I am sure there are cases where the requirements of
the system are so clear that one can write the "blueprint" down ahead
of time.  But in our case, when one is creating something totally new
and trying to do it quickly, it becomes necessary to draw the
blueprint and build the house simultaneously.  It is not surprising
that when doing that there is a cost, which is refactoring the
codebase or even rewriting portions of it.
