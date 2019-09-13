---
layout: post
title:      "Hypothesis Testing: Significance Level and ANOVA test"
date:       2019-09-11 22:54:37 -0400
permalink:  hypothesis_testing_significance_level_and_anova_test
---


This post is going to discuss about significance level and ANOVA test.

In hypothesis testing,  the null hypothesis is a general statement or default position that there is nothing new happening, it is denoted by H0.

Alternative hypothesis is a position that states something is happening, a new theory is true instead of an old one (null hypothesis). It is denoted by H1 or Ha.

Significance level is the basis of every test. Without significance level, nothing can be tested about null hypothesis and hence no conclusions can be drawn.

A significance level should be defined before performing any tests, so that it is not modified based on the desire to accept or reject the null hypothesis. Formally, a significance level is defined as is the probability of the study rejecting the null hypothesis, given that the null hypothesis were assumed to be true.

Significance level is typically set to 5% or lower. The result of a test is statiscally significant and the null hypothesis is rejected, if the p-value is less than the significance level.

If a signficance level is set to lower, such as 1% or 0.1%, it is less likely to be affected by random chance.  In some scientific research, it can be as low as 10^(-7).



ANOVA test stands for Analysis of Variance. It is widely used when there are multiple variables that can affect the target variable. 

It is very convenient to run ANOVA test in order to find out which ones of the independent variables have signficant effect on the target. It also supports categorical variables without one-hot encoding needed. An example is shown here.

```
formula = 'Quantity ~ C(CategoryId)'
lm = ols(formula, orders).fit()
sm.stats.anova_lm(lm, typ=2)
```

Sample result:
```
                      sum_sq      df         F    PR(>F)
C(CategoryId)    1292.377084     7.0  0.509429  0.828058
Residual       778107.259110  2147.0       NaN       NaN
```

If the probability is less than the significance level, the null hypothesis is rejected.


Definition Source: Wikipedia

