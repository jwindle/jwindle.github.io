---
layout: page
title: About
permalink: /about/
---

Previously, I was Director of Data Science at [Hi Fidelity
Technologies (HFT)](https://www.hifidelitytechnologies.com/), where I
helped invent a novel root sensing device, called RootTracker, and
build out its data platform.  RootTracker could monitor the root
systems' of thousands of plants simultaneously and, for the first
time, enabled the optimization of root systems for improved nutrient
uptake, stress tolerance, and reduced greenhouse gas emissions.  

Below you will find a brief recapitulation of my skills and work
experience.  You can also find me on
[LinkedIn](https://www.linkedin.com/in/jesse-windle-19802836).


## Prior work and training

- 2015-2023: Director of Data Science, [Hi Fidelity Genetics /
  Technologies](https://www.hifidelitytechnologies.com/)
- 2014-2015: Visiting Assistant Professor, Duke University

- Postdoc: Duke University, Statistics, 2014
- PhD: University of Texas at Austin, Comp. and Appl. Mathematics, 2013
- BS: University of Nebraska – Lincoln, Mathematics, 2005


## Selected skills
		
**Data Science**: Non-parametric models (i.e. neural networks, random
forests, Gaussian processes), structured Bayesian modeling, standard
tools like linear and mixed models, R, and Python.
		
**Systems Engineering and Development**: RESTful Flask-based API,
Postgres, Apache Iceberg.
		
**Scientific Communication**: Reducing complex data to key metrics;
conveying results in high-level, graphical summaries.

**Quantitative Genetics**: Genomic prediction with DNA and RNA data.


## Selected professional experiences

- **[Invented](https://patents.google.com/patent/US11293910B2/) a
  device, called RootTracker, to measure root systems at scale**
  
    Measuring root growth in the field has historically been a
    challenge, which has limited the use of root characteristics as a
    target of crop improvement.  To overcome this problem, I invented
    a device that uses capacitance touch sensors to measure root
    systems at scale.  This pioneering device enabled the optimization
    of root systems for improved nutrient uptake, stress tolerance,
    and greenhouse gas reduction.  (You can read the patent
    [here](https://patents.google.com/patent/US11293910B2/).)
  
- **[Recapitulated](../2023/07/26/rootmodel.html) root growth using
  RootTraker data**

	For a species like corn, one can think of a root growing as a
    random walk.  A root starts from where the stem touches the soil
    and then meanders outwards and down.  RootTracker could tell us
    one point along this random walk, which is very limited
    information as to the appearance of the entire root.  However,
    using a highly structured model I recreated realistic
    recapitulations of root growth from these data that captured the
    temporal and spatial patterns of the underlying ground truth.
    (You can read more [here](../2023/07/26/rootmodel.html).)

- **Built the RootTracker [data platform](../2023/08/09/data-engineering.html)**
  
    For a single device, RootTracker captured data every 5 minutes.
    Thousands of devices might stream data in a single season.  I
    helped build a system to capture these sensor data and track our
    experiments.  A Flask-based API provided access to the data, which
    was modeled using a mixture of SQL and Apache Iceberg.  A Voila
    App assisted with data exploration, visualization, and analysis.
    (You can read more [here](../2023/08/09/data-engineering.html).)

- **Analyzed all internal and client trials**

	HFT conducted experiments for itself and others, including ag
    majors BASF, Bayer, and Corteva.  I was responsible for analyzing
    and communicating the subsequent results.  For both internal and
    external projects, this involved establishing the scientific
    questions of interest, data exploration and analysis, and then
    communicating results, usually in the form of a presentation or
    report.

- **Built out the team and company**

	As employee #1, I helped build the company from the ground up ---
    inventing the technology, assembling the early team, and then
    overseeing our data engineering, device engineering, and data
    science teams as the company grew.  Through the writing of grants,
    I helped raise over $2 million in non-dilutive funding.
		
		

		
