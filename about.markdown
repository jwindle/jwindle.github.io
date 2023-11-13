---
layout: page
title: About
permalink: /about/
---

Previously, I was Director of Data Science at the pioneering startup
[Hi Fidelity Technologies
(HFT)](https://www.hifidelitytechnologies.com/), where I helped invent
a novel root sensing device, called RootTracker, and build its data
management and analysis platform.  RootTracker could monitor the root
systems' of thousands of plants simultaneously and, for the first
time, enabled the optimization of root systems for improved nutrient
uptake, stress tolerance, and reduced greenhouse gas emissions.  

I am currently engaged as a contractor into 2024.  Beyond that, I am
interested in an early stage project that is looking to operationalize
a data thesis.  I am also interested in joining a data science team
working on a complex, big data problem.

Below you will find an overview of my skills and work experience.  You
can also find me on
[LinkedIn](https://www.linkedin.com/in/jesse-windle-19802836).


## Prior work and training

- 2015-2023: Director of Data Science, [Hi Fidelity Genetics /
  Technologies](https://www.hifidelitytechnologies.com/)
- 2014-2015: Visiting Assistant Professor, Duke University

- Postdoc: Duke University, Statistics, 2014
- PhD: University of Texas at Austin, Comp. and Appl. Mathematics, 2013
- BS: University of Nebraska – Lincoln, Mathematics, 2005


## Selected skills

**Methods**: Bayesian analysis, neural networks, random forests, kernel machines, linear and mixed models, hypothesis testing, time series

**Software**: Python, R, C++, SQL, Iceberg, Bash / Linux, AWS, Git

(Common Python & R packages: numpy, pandas, scipy, sklearn,
statsmodels, pytorch, jax, sqlalchemy, pymongo, flask, pytest; rstan,
tidyverse [e.g. ggplot2, dplyr, readr], lme4, kernlab, spaMM,
quantreg, glmnet, bayeslogit, randomForest, etc., etc., etc.)

**Scientific Communication**: Reducing complex data to key metrics;
conveying results in high-level, graphical summaries.


## Selected professional experiences

- **[Invented](https://patents.google.com/patent/US11293910B2/) a
  device, called RootTracker, to measure root systems at scale**
  
    Measuring root growth in the field has historically been a
    challenge, which has limited the use of root characteristics as a
    target of crop improvement.  To overcome this problem, I invented
    a device that uses capacitance touch sensors to measure root
    systems at scale.  This novel device enabled the optimization of
    root systems for improved nutrient uptake, stress tolerance, and
    greenhouse gas reduction.  (You can read the patent
    [here](https://patents.google.com/patent/US11293910B2/).)
  
- **[Inferred root growth](../2023/07/26/rootmodel.html) using
  RootTracker data**

	For a species like corn, one can think of a root growing as a
    random walk.  A root starts from where the stem touches the soil
    and then meanders outwards and down.  RootTracker could tell us
    one point along this random walk, which is very limited
    information as to the appearance of the entire root.  Using
    statistical modeling I was able to overcome this limitation to
    recreate realistic recapitulations of root growth from these data
    that captured the temporal and spatial patterns of the underlying
    ground truth.  (You can read more
    [here](../2023/07/26/rootmodel.html).)

- **[Learned root
  phenotypes](../2023/11/01/ai-for-root-phenotyping.html)** using AI

  One of the challenges in developing our technology was identifying
  ground truth.  I developed a novel approach using AI to extract root
  phenotypes.  It relied on conducting experiments where the outcome
  was effectively "plant" or "no plant".  Using a neural network
  trained on that outcome, it is possible to extract an intermediate
  layer that corresponds to root detections.  (You can read more
  [here](../2023/11/01/ai-for-root-phenotyping.html).)

- **Built the RootTracker [data platform](../2023/08/09/data-engineering.html)**
  
    For a single device, RootTracker captured data every 5 minutes.
    Thousands of devices might stream data in a single season.  I
    helped build a system to capture these sensor data and track our
    experiments.  A Flask-based API provided access to the data, which
    was modeled using a mixture of SQL and Apache Iceberg.  A Voila
    App enabled data exploration, visualization, and analysis.  (You
    can read more [here](../2023/08/09/data-engineering.html).)

- **Produced [results](../2023/09/12/rtda.html) for all internal and client trials**

	HFT conducted experiments for itself and others, including ag
    majors BASF, Bayer, and Corteva.  I was responsible for analyzing
    and communicating the subsequent results.  For both internal and
    external projects, this involved establishing the scientific
    questions of interest, data exploration and analysis, and then
    communicating results as a presentation or report.  In one of our
    most exciting studies, I was able to show that the amount of roots
    present in the root crown was inversely related to nitrous oxide
    emissions, a major greenhouse gas emitted by row crop agriculture.
    (You can read more [here](../2023/09/12/rtda.html).)
	
- **Predicted performance of maize hybrids**

	HFT had a proprietary breeding program.  I used DNA data to
    predict the performance of untested varieties using measurements
    from related plants.

- **Built out the team and company**

	As employee #1, I helped build the company from the ground up ---
    inventing the technology, assembling the early team, and then
    overseeing our data engineering, device engineering, and data
    science teams as the company grew.  Through the writing of grants,
    I helped raise over $2 million in non-dilutive funding.
		
		

		
