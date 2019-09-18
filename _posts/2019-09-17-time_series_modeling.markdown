---
layout: post
title:      "Time Series Modeling"
date:       2019-09-17 15:00:11 -0400
permalink:  time_series_modeling
---


How to predict the future with past data? This is what time series forecasting is about.

In Module 4 project, my task is to act as a consultant for a real estate investment firm. The dataset contains data obtained from Zillow research with home prices in 14723 zip codes from April 1996 to April 2018. That is 22 years of data.

Some of the zip codes have missing data. There is no good way to project those missing values, hence I removed them from the data set. After dropping null rows, there are 12895 zip codes remaining.

I calculated the rate of return by comparing the price in April 2018 and January 2013. The coefficient of variation is also calculated by standard deviation divided by mean.

Only places with <=0.35 coefficient of variation is retained, and sorted by rate of return.

The top 25 results are put into ARIMA model to predict the price 5 years later, in April 2023.

The problem with ARIMA model is its slow speed. It takes several minutes to process all 25 inputs.

```
0	30238	102900.0	184913.202615	79.701849	GA	Jonesboro	Atlanta
1	28208	113400.0	201593.664970	77.772191	NC	Charlotte	Charlotte
2	37207	200800.0	346858.740690	72.738417	TN	Nashville	Nashville
3	89433	272600.0	452048.357727	65.828451	NV	Sun Valley	Reno
4	89431	250900.0	404620.429615	61.267608	NV	Sparks	Reno
5	80010	277600.0	433940.347896	56.318569	CO	Aurora	Denver
6	89502	281200.0	430488.320618	53.089730	NV	Reno	Reno
7	89506	279400.0	426310.343296	52.580653	NV	Reno	Reno
8	89503	310200.0	451825.354314	45.656143	NV	Reno	Reno
9	48239	97600.0	139618.737246	43.051985	MI	Redford	Detroit
```

The columns are zip code, 2018 price, 2023 projected price, % increase, state, city and metro.

Notice that 5 of the top 10 are from Reno area. For diversification, I replaced 5th place 89431 with 6th place 80010 from Colorado.

Here are the projection plots:

![](https://i.imgur.com/HKczOyw.png)
![](https://i.imgur.com/GG3LHLf.png)
![](https://i.imgur.com/waJPUAe.png)
![](https://i.imgur.com/HKczOyw.png)
![](https://i.imgur.com/6ntU2bo.png)

The ARIMA model does not have the ability to predict prices going down in this situation. I want to try out other time series models in the future and compare the results.
