---
toc: true
layout: post
description: Statistics Blog Posts
categories: [Statistics]
title: T-Tests The Purpose, Assumptions, How it Works, and Corrections.
---




![](https://upload.wikimedia.org/wikipedia/commons/7/74/Normal_Distribution_PDF.svg "Credit: Wikipedia")

## Purpose:

The purpose of the T-test is to compare if there are mean differences between two groups of interest. 

## Assumptions:
+ Normal distribution of the dependant variable
+ Independent and identically distributed (i.i.d) variables

## How it works:
T-test comparisons use the means, counts and standard deviations of a treatment and control in comparison to an idealized normal distribution to calculate a p value, which by intuition is the likelihood of seeing a mean difference of the same or more extreme magnitude between treatment and control as a result of chance. This is done through a comparison to an idealized normal distribution, through the calculation of a t-statistic. While the test statistic is assumed to follow an idealized normal distribution if the scaling term is known, where the scaling term is unknown and it is instead estimated based on the data, which is assumed to follow the student's t distribution. This process can be thought of trying to disentangle the signal (mean difference and counts) from the noise variability. Here the mean difference is the direction of the signal and the counts are the strength of the signal.

## Corrections:
When we are interested in comparing statistical differences between more than two groups, we may use ANOVA, but if we want to compare differences between more than a single pairwise comparison, we can conduct multiple t-tests. In doing so, we will end up increasing the likelihood of a false positive (type I error) where we are incorrectly rejecting the null hypothesis that there are no statistical differences between groups. One way to address this is to use the Bonferroni correction.

### Bonferroni Correction

The Bonferroni correction, the namesake of Carlo Emilio Bonferroni, accounts for what we lose in a p-hacking quest in the experimentation, which is the justification for taking p-values at face value. By intuition, when we go searching for significant differences everywhere, the chance of seeing an apparent significant difference by chance anywhere increases. Using the Bonferroni correction, if the starting alpha/significance level is .05 and we are testing 10 hypotheses, then the corrected alpha/significance level we should use would be .005. Understanding the lack of an incentive to make such an adjustment is straightforward. Another way to address this is to first use ANOVA to detect statistical differences between all groups before deciding whether to use t tests to look for pairwise comparisons between groups.




```
python ttest.py
```
