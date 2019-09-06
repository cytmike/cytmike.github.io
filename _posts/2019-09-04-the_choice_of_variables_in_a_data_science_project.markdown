---
layout: post
title:      "The Choice of Variables in a Data Science Project"
date:       2019-09-04 23:05:23 -0400
permalink:  the_choice_of_variables_in_a_data_science_project
---


My first data science project is to predict housing prices in King County, WA. It is interesting because I am living in King County. The data set contains 21597 sales record between May 2014 and 2015. 

In this blogpost, I am going to describe my process to decide what variables to include in the regression model. Data cleaning is an important step in any data science project.

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
Similarly, floor has 6 discrete values: 1.0, 1.5, 2.0, 2.5, 3.0 and 3.5. It can also be converted to categorical variable.

long, yr_built, sqft_lot15, and sqft_lot are dropped because of low correlation to price.

yr_renovated can be converted to a boolean to indicate if a house was renovated. It is because the year itself has little meaning. This plot shows that renovation has an effect on the price.
![](https://i.imgur.com/gcMjfTt.png)

Thus the model will include 6 numerical variables: bedrooms, bathrooms, grade, sqft_above, sqft_basement and lat.

Then there are 2 boolean variables , that has 0 or 1 value, waterfront and renovated.

The rest are categorical variables, converted from zipcode, view, floors and condition.
The regression model will compute the price of any given house using these variables.

Here are the list of all variables:
```
Index(['bedrooms', 'bathrooms', 'waterfront', 'grade', 'sqft_above',
       'sqft_basement', 'lat', 'renovated', 'zipcode_98002', 'zipcode_98003',
       'zipcode_98004', 'zipcode_98005', 'zipcode_98006', 'zipcode_98007',
       'zipcode_98008', 'zipcode_98010', 'zipcode_98011', 'zipcode_98014',
       'zipcode_98019', 'zipcode_98022', 'zipcode_98023', 'zipcode_98024',
       'zipcode_98027', 'zipcode_98028', 'zipcode_98029', 'zipcode_98030',
       'zipcode_98031', 'zipcode_98032', 'zipcode_98033', 'zipcode_98034',
       'zipcode_98038', 'zipcode_98039', 'zipcode_98040', 'zipcode_98042',
       'zipcode_98045', 'zipcode_98052', 'zipcode_98053', 'zipcode_98055',
       'zipcode_98056', 'zipcode_98058', 'zipcode_98059', 'zipcode_98065',
       'zipcode_98070', 'zipcode_98072', 'zipcode_98074', 'zipcode_98075',
       'zipcode_98077', 'zipcode_98092', 'zipcode_98102', 'zipcode_98103',
       'zipcode_98105', 'zipcode_98106', 'zipcode_98107', 'zipcode_98108',
       'zipcode_98109', 'zipcode_98112', 'zipcode_98115', 'zipcode_98116',
       'zipcode_98117', 'zipcode_98118', 'zipcode_98119', 'zipcode_98122',
       'zipcode_98125', 'zipcode_98126', 'zipcode_98133', 'zipcode_98136',
       'zipcode_98144', 'zipcode_98146', 'zipcode_98148', 'zipcode_98155',
       'zipcode_98166', 'zipcode_98168', 'zipcode_98177', 'zipcode_98178',
       'zipcode_98188', 'zipcode_98198', 'zipcode_98199', 'view_1.0',
       'view_2.0', 'view_3.0', 'view_4.0', 'condition_2', 'condition_3',
       'condition_4', 'condition_5', 'floors_1.5', 'floors_2.0', 'floors_2.5',
       'floors_3.0', 'floors_3.5'],
      dtype='object')
			```
