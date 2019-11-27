---
layout: post
title:      "Expected Goals Model in Assocication Football"
date:       2019-11-27 20:28:33 +0000
permalink:  expected_goals_model_in_assocication_football
---


After hearing a talk on Data Science in football presented by Dr. Spearman from Liverpool FC, I decided to do something about football analytics myself.

Expected Goals is an interesting concept that gets into the media. It is not uncommon to hear about xG on TV nowadays. I am developing an xG model on my own using shots data.

After comparing several algorithms, it is the best to use Neural Network. It has an accuracy of over 91%.

xG does not consider anything about the teams, or the individual players. It is treating anybody to have the same skillset. For the same shot attempt, Ronaldo and me have the same xG value by the model. 

As a result, the teams or players who outperform the xG values are considered the best.

It is fun to see that the model can confirm facts that we know, such as Ronaldo is the best at headers and Messi is best at left foot shots, by a very wide margin.

In the future, I would like to improve the model by including newer data beyond 2017. It is also interesting to see why no teams or players from Premier League appear at the top of the list.
