---
title: Cognition in an Aging Popultation
author: Olivia Wilcox
date: '2022-03-23'
slug: cognition
categories: []
tags: []
subtitle: 'Data analysis using the HRS publice dataset'
summary: ''
authors: []
lastmod: '2022-03-23T11:44:01-04:00'
featured: no
image:
  caption: ''
  focal_point: ''
  preview_only: no
projects: []
---

Using 2018 Core data from the Health and Retirement Study by the University of Michigan, I created a set of regression models to analyze cognitive impairment within the 65+ age group.

I created the variable `animals` to use as my quantitative outcome variable, which represents the Animal Naming Test (ANT). This is a popular verbal fluency test used by neuropsychologist to assess cognitive functioning. In the ANT, patients are asked to list as many animals as possible in 60 seconds and the interviewer writes down the number of correctly named and uniquely identified animals. Scores below 14 are considered a sign of cognitive impairment.

Here is a look at the distribution of the `animals` variable:








<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-4-1.png" width="672" />


We can see that scores ranged from 1 to 40.

One of the questions in HRS asks patients to rate their memory at the present time. I was interested in if there was an association in the subject's perception of their memory and their score on the ANT. Furthermore, I wanted to know if I could predict the number of `animals` a subject in the HRS could name in 60 seconds, after adjusting for `memory`, `sex`, `age`, and `health`.

# Codebook

Variable | Role | Type | Description
-------- | ---- | ---- | -----------------
`ID`    | identifier | - | character code for subjects
`animals` | outcome | quant | number of animals listed in 60 seconds
`memory` | input | 3-cat | rate your memory at the present time (great, good, poor)
`sex`   | input | 2-cat | biological sex (male, female)
`age`   | input | want | age in years
`health` | input | 3-cat | rate your health (great, good, poor)


I created a main effects using `memory`, `age`, `sex`, and `health` to predict `animals`.




Here are the coefficients and confidence intervals for my main effects linear regression model.


|term        | estimate| std.error| conf.low| conf.high|
|:-----------|--------:|---------:|--------:|---------:|
|(Intercept) |   34.760|     1.781|   31.266|    38.255|
|memorygood  |    0.493|     0.489|   -0.466|     1.452|
|memorypoor  |   -1.333|     0.532|   -2.376|    -0.290|
|age         |   -0.213|     0.022|   -0.257|    -0.169|
|sexfemale   |   -0.142|     0.368|   -0.863|     0.580|
|healthgood  |   -1.435|     0.442|   -2.302|    -0.568|
|healthpoor  |   -3.333|     0.479|   -4.273|    -2.394|


By looking at the cofficients, we can see my model predicts that a subject who reported  their `memory` as poor will score 1.3 points lower on the ANT than a subject who reported their `memory` as great. Additionally, my model predicts that a subject who reported their `health` as poor will score 3.3 points lower on the ANT than a subject who reported their `health` as great.

I'm not surprised that scores were predicted to decrease as the patient reported outcome (`memory` or `health`) decreased, but I am surprised that the effect size isn't larger. A decrease in 1 to 3 points isn't that much, especially considering I thought these predictors would be closely related to visual spatial memory outcomes.

Finally, here are the residual plots. We can see that there were no major problems with residual assumptions for this model.

<img src="{{< blogdown/postref >}}index_files/figure-html/unnamed-chunk-7-1.png" width="672" />
