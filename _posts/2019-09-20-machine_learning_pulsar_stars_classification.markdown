---
layout: post
title:      "Machine Learning: Pulsar Stars Classification"
date:       2019-09-20 17:14:39 -0400
permalink:  machine_learning_pulsar_stars_classification
---


Pulsar candidates were collected from the High Time Resolution Universe Survey. Pulsars are a type of star, first discovered in 1967. Candidates must be classified into pulsar and non-pulsar classes to aid discovery. Machine learning algorithms are used for classification in this project.

When I studied Astronomy classes in college, I already heard that most of the time researchers were dealing with numbers and data instead of photos. Photographs are mostly only for amateurs or hobbyists.

Now I get my own chance to analyse this Astronomy problem, using my data science skills.


Different machine learning algorithms were used in this project. They are Logistic Regression,
K-nearest Neighbors,
Support Vector Machines,
Adaboost,
Gradient Boosting, and
Random Forest. There is no one single algorithm which performs the best all the time, so it is interesting to check with multiple algorithms.

Logistic Regression is the best algorithm at 98.16%, while Adaboost comes in second at 98.01%.

One difficulty that I encountered is it was too slow to run any grid searches. It could not be completed in any reasonable timeframe.


References

R. J. Lyon, B. W. Stappers, S. Cooper, J. M. Brooke, J. D. Knowles, Fifty Years of Pulsar Candidate Selection: From simple filters to a new principled real-time classification approach, Monthly Notices of the Royal Astronomical Society 459 (1), 1104-1123, DOI: 10.1093/mnras/stw656

R. J. Lyon, HTRU2, DOI: 10.6084/m9.figshare.3080389.v1.
