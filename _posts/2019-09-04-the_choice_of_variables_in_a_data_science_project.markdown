---
layout: post
title:      "The Choice of Variables in a Data Science Project"
date:       2019-09-04 23:05:23 -0400
permalink:  the_choice_of_variables_in_a_data_science_project
---


My first data science project is to predict housing prices in King County, WA. It is interesting because I am living in King County. The data set contains 21597 sales record between May 2014 and 2015. 

In this blogpost, I am going to describe my process to decide what variables to include in the regression model.

The dataset is from Kaggle. https://www.kaggle.com/harlfoxem/housesalesprediction

Here is a preview of the 21 columns:

```
<class 'pandas.core.frame.DataFrame'>
RangeIndex: 21597 entries, 0 to 21596
Data columns (total 21 columns):
id               21597 non-null int64
date             21597 non-null object
price            21597 non-null float64
bedrooms         21597 non-null int64
bathrooms        21597 non-null float64
sqft_living      21597 non-null int64
sqft_lot         21597 non-null int64
floors           21597 non-null float64
waterfront       19221 non-null float64
view             21534 non-null float64
condition        21597 non-null int64
grade            21597 non-null int64
sqft_above       21597 non-null int64
sqft_basement    21597 non-null object
yr_built         21597 non-null int64
yr_renovated     17755 non-null float64
zipcode          21597 non-null int64
lat              21597 non-null float64
long             21597 non-null float64
sqft_living15    21597 non-null int64
sqft_lot15       21597 non-null int64
dtypes: float64(8), int64(11), object(2)
memory usage: 3.5+ MB
```

First of all, id is unrelated to the regression, and price is the target variable.

sqft_basement is stored as a string, and it can be converted to a number, after filling null values.

There are a large number of dates, we want to see if they can be grouped by months.

![](https://i.imgur.com/efJDNsF.png?1)

It turns out that there is no relationship between months and price of a house. The date column can also be dropped.


The zip codes also have no meaning numerically. They can be converted to categorical variables. Here is a plot of average selling price for each zip code.
![](https://i.imgur.com/wLS1Dkj.png)

The next step in modeling is to check for multicollinearity. This is because regression assumes the variables are unrelated to each other. Here is a heatmap.
![](https://i.imgur.com/nkT6NIS.png)


sqft_living, bathrooms, sqft_living15 and sqft_above are highly correlated, so it is reasonable to remove some of them. In this model, sqft_living15 and sqft_living are removed. sqft_above and bathrooms are retained because they are more intuitive to understand.

Next step is to check for linearity. If a variable does not have a linear relationship with price, it cannot forecast price in regression. Such variables should be dropped.

One such example would be zipcode. An increase of decrease in zipcode have no relationship with the price.

The correlation of each variable with price is calculated below.

```
long             0.022036
condition        0.036056
yr_built         0.053953
sqft_lot15       0.082845
sqft_lot         0.089876
yr_renovated     0.117855
floors           0.256804
waterfront       0.264306
lat              0.306692
bedrooms         0.308787
sqft_basement    0.321108
view             0.393497
bathrooms        0.525906
sqft_above       0.605368
grade            0.667951
```

view and condition can be converted to categorical variable, because they are discrete values from 0 to 5.

long, yr_built, sqft_lot15, and sqft_lot are dropped because of low correlation to price.

yr_renovated can be converted to a boolean to indicate if a house was renovated.
