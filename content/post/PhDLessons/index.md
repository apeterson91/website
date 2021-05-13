---
date: 2021-05-05
title: "PhD Lessons Learned"
summary: "A few lessons learned along the way in completing my PhD"
tags: ["Statistics"]
author: "Adam Peterson"
markup: mmark
image:
  placement: 1
  caption: ""
  focal_point: "Center"
  preview_only: true 
---


# Preface

I’m offering the following key observations on things I learned in my PhD as a way of documenting for myself some of my major lessons learned. 
It is also my hope that others may find it useful as a kind of reference list from which they might learn, as I have greatly benefited from other PhD students or professor’s documentation of similar references and tools.


# Philosophical 

Few different layers here worth exploring
(1) Personal Attitude
(2) Approach to Problem, or Research Philosophy  and
(3) Statistical Philosophy.


## (1) Personal Attitude

One’s personal attitude towards the PhD will define everything else learned from it. One key lesson worth learning early on is to let go of your ego. 
This is easier said than done, as everyone in academia care’s a lot about their intelligence – obviously. 
That’s how we got to be in graduate school after all – so learning to accept that you’re not that smart and that there’s still a lot one has to learn before becoming a peer of the academy can take some getting used to.
Further, it helps to be acclimated to the lifestyle. You 
need to be very self-driven to get a PhD, as there is much less structure as compared to a M.S. program and one’s experience is largely determined by what the student makes of it.
This means that while, yes you can get up any time you want in the day, it helps if you’re self-disciplined enough to get up at such a time that you still get the things done that you need to in order to make progress in your research.


## (2) Approach to the Problem; Research Philosophy 

There’s two things to think about under this heading: (i) The Science (referring to a specific branch of science) and (ii) the Statistics

(i) This is where a statistician would typically collaborate with “subject-matter experts”. That is, other scientists who are more familiar with the conceptual models, standards in the field and so on that define the current state of knowledge and research within the domain of study. Questions in this domain may follow fairly easily from the questions that are most often posed in the literature, or they may be more subtly hidden.

(ii) Concerns research that extends old or develops new statistical ideas for the purposes of providing statisticians with more tools to model natural phenomenon. E.g. creating a new distribution on the space of some species of graphs I’d consider to be something like “Pure” Statistics research. It may be the case (for the better) that this developed with an application in mind and so the statistical idea may be merely an adaptation or tweaking of previously established methods to a new kind of data structure or problem. Both would fall under the heading of what’s called “Method’s Research”


## (3) Statistical Philosophy


My foundational training was in what is commonly referred to as “classical” or Frequentist statistics. 
There’s good reason for this as this approach laid the groundwork for much of the applied statistical work that is done today. 
From the get-go though, I was interested in and hearing about the “new kid on the block”: Bayesian statistics. 
Of course, this philosophy isn’t all that new, with the first documented work describing Bayesian statistics, going way back to the 1700s, with a work authored by Laplace. 
I found there to be a number of reasons Bayesian statistics is worth learning in the modern era, principal among them the phenomenon of "concentration of measure", which
provides evidence to suggest that the posterior mode (the frequentist's maximum likelihood estimate) is not an "appropriate" description of the posterior distribution in 
high dimensional spaces. As high dimensional spaces characterize a lot of the work in advanced statistics, this is of increasing importance. There is a nice [case study](https://mc-stan.org/users/documentation/case-studies/curse-dims.html) by Bob Carpenter,
that tries to provide intuition for these ideas via simulation, as well as a more technical discussion of these ideas [here](https://discourse.mc-stan.org/t/concentration-of-measure-and-typical-sets/2786) in the stan forums.


# Conceptual Workflow 


### Working on methods?

Think about the question you’re trying to answer. Think long. Think hard.

Some things you might do to guide your thinking:

* Brainstorm on established statistical methods/techniques = read literature
* Write simple theoretical models down
* Run simple simulations to jog intuition

Think you’ve got a worthy idea? Run it by someone else if possible, regardless run it in the lab:

 * Run a simple simulation - does the generating data make sense?
 * Does the model make sense? Can the model recapture the data?
 * Start making a package to document the development of your code used to estimate the model

Document your simulation progress using vignettes/markdown notebooks - they’ll make it easy to refer back to. Try to version everything with git to make it easier to keep track of.

### Working on an analysis?

* Think about the question you’re trying to answer. Typically this is more concretely defined than in the broad methods setting since here, you’re likely to use a more standard method.
* Run descriptives, make simple plots at first (fancier plots after :-D )
* Come up with a model that answers or approximates the question as best possible with the available data (consider more idyllic data/experimental setting as well in your documentation)
* Follow (with judicious liberality) the workflow in Gelman et al.’s 2020 “Bayesian workflow” - using reproducible tools if possible
 * At most this includes a git versioned R project with data manipulation, modelling, and presentations all documented and included for future modification and reference
 * Jeff Leek has some good writing on this subject. You can check out his [book](https://leanpub.com/modernscientist) or his [github](https://github.com/jtleek) repos that touch on these topics in different ways.


# Technical

You read a lot of textbooks in grad school. Some are good, others aren’t. Here are the ones I continue to reference after first exposure.


#### Statistics:

* Casella and Berger (2nd edition 2001)
* Bayesian Data Analysis (Gelman et al. 3rd edition 2013)
* Regression and Other Stories (Gelman et al. 2020)
* Applied Longitudinal Analysis (Fitzmaurice & Laird 2008)
* Hierarchical Modeling and Analysis for Spatial Data (Banerjee, 2004)
* Generalized Additive Models: an Introduction with R (Wood, 2016)
* Causal Inference – What if? (Hernan and Robins 2020)
* Mastering Metric (Angrist & Pischke 2014)
* The Matrix Cookbook (Petersen 2012)
* Handbook of Markov Chain Monte Carlo (Brooks et al. 2011)
* Machine Learning: A Probabilistic Perspective (Murphy 2013)


#### Computational:

* [R for data science](https://r4ds.had.co.nz/) (Wickham and Grolemund)
* [R packages](https://r-pkgs.org/) (Wickham)
* [Advanced R](https://adv-r.hadley.nz/)  (Wickham)
* C++ Primer (Lipmann et al. fifth edition)
* [Rcpp for everyone](https://teuder.github.io/rcpp4everyone_en/) (Tsuda)
* [Geocomputation with R](https://geocompr.robinlovelace.net/) (Lovelace)


##### R packages

Rstudio has a good list of well supported R packages across a wide range of domains [here](https://support.rstudio.com/hc/en-us/articles/201057987-Quick-list-of-useful-R-packages).

Here are the (non-specialized) R packages I’ve come to use regularly.

* Drake + dflow (currently transitioning to [targets](https://github.com/ropensci/targets) + [tflow](https://github.com/MilesMcBain/tflow))
* [Tidyverse](https://www.tidyverse.org/) of course
* The [brms](https://paul-buerkner.github.io/brms/) package for most “standard” bayesian modeling - E.g. Bayesian (potentially hierarchical) glms
* The [rstan](https://mc-stan.org/users/interfaces/rstan) package for some “non-standard” bayesian modeling
* [Rcpp](https://rcpp.org) (and associated Rcpp packages like RcppEigen, RcppProgress,RcppParallel) for other “non-standard” bayesian models. 
* -- It can often help to read the code of other developers working in this space, as well as R in general
* The [gtsummary](http://www.danieldsjoberg.com/gtsummary/) package for paper/presentation tables
* -- I sometimes use [gt](https://gt.rstudio.com/) directly

For making other packages:
* [usethis](https://usethis.r-lib.org/)
* [devtools](https://devtools.r-lib.org/) (including roxygen2, etc.)
* [renv](https://rstudio.github.io/renv/articles/renv.html) - can also be useful for analyses potentially



Specialized R Packages I use for spatial analysis:

* The [sf](https://r-spatial.github.io/sf/) package
* The [fields](https://github.com/NCAR/fields) package
* The [spatstat](http://spatstat.org/) package
* The [ggmap](https://github.com/dkahle/ggmap), or [leaflet](https://rstudio.github.io/leaflet/) packages for visualization
