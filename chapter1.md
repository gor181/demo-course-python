---
title: 'Key Performance Indicators: Measuring Business Success'
description: >-
    This chapter provides a brief introduction to the content that will be covered throughout the course before transitioning into a discussion of Key Performance Indicators or KPIs. Specifically we discuss how to identify and define meaningful KPIs through a combination of critical thinking and leveraging Python and Pandas tools. These techniques are all presented in a highly practical and generalizable way. Ultimately these topics serve as the core foundation for the A/B testing discussion that follows. 
---

## Course Introduction and Overview

```yaml
type: VideoExercise
lang: python
xp: 50
skills: 2
key: 03f18ef5fd
```

This lesson provides an overview of the topics that we will be discussing throughout the course. Specifically focusing on what A/B testing is and why it is important. The lesson concludes with a brief introduction to Key Performance Indicators, the primary focus of this Chapter. 


`@video_link`

//player.vimeo.com/video/154783078

`@video_hls`

//videos.datacamp.com/transcoded/000_placeholders/v1/hls-temp.master.m3u8

`@projector_key`
3045ddfcd8a882a51ace27f9ec851daa

---
## Understanding the Key Components of an A/B test

```yaml
type: PureMultipleChoiceExercise
key: 054f171b8e
xp: 50
skills: 2
```
From our discussion so far, which of the following do you think is the key component of an A/B tests usefulness?

`@possible_answers`
- Having exactly the same size test and control group. 
- [Having the users be randomly assigned to groups.]
- Running the test for at least three weeks. 
- Having an equal number of males and females in each group.

`@hint`
Think about how hard it would be in practice to ensure the groups were exactly equal in size and composition. 

`@feedback`
- While the groups should be similar in size, there is no need for them to be exactly the same size.
- Correct! Randomness helps ensure nothing else is impacting our observed results.
- Each test will need to be run for a different length of time. There is no general rule guiding this across tests. 
- Ideally we want our groups to be similarly composed, but an identical composition is not needed. 

---
## Defining Meaningful KPIs

```yaml
type: PureMultipleChoiceExercise
key: 407c62374a
xp: 50
skills: 2
```
Identify which of the following would **not** be a meaningful KPI for a small foodtruck trying to optimize its business? 

`@possible_answers`
- Customers served per hour 
- Average profit per meal sold 
- Revenue lost in food waste per day
- [Meals sold over the past year]

`@hint`
Put yourself in the shoes of running this business. What would not be specific and granular enough to let you make good decisions. 

`@feedback`
- This is a solid KPI, it would help you to optimize your efficiency in serving customers.
- This is a great and common metric. Many businesses rely profit per unit sold as a KPI. 
- This metric, while somewhat specific to this business, would be helpful in cutting costs in a practical way.
- Correct! For some businesses yearly metrics are useful. But for a food truck trying to optimize its sales this is too long of a period. 

---
## Identifying and Understanding KPIs
```yaml
type: VideoExercise
lang: python
xp: 50
skills: 2
key: 1b4481f114
```

This lesson continues our discussion of KPIs by working through an example dataset. We will discuss how to think about defining a KPI for a particular set of data while beginning to analyze the example dataset using the pandas `.merge()` method. 

`@video_link`

//player.vimeo.com/video/154783078

`@video_hls`

//videos.datacamp.com/transcoded/000_placeholders/v1/hls-temp.master.m3u8

`@projector_key`
10d614190e79f5a22314e1b7f6536601


---
## Loading & Examining Our Data

```yaml
type: NormalExercise
key: 42085ab088
lang: python
xp: 100
skills: 2
```

In this exercise, you will start working with the Pandas library by loading and examining two datasets. One contains a set of user demographics and the other is a set of data relating to in-app purchases for our metidation app.

`@instructions`
- Import the pandas package as `pd`.
- Load the file `customer_data.csv` as a dataFrame called `customer_data`.
- Load the file `inapp_purchases.csv` as a dataFrame called `app_purchases`.
- Output the top rows of our `customer_data` dataFrame using the `.head()` method.

`@hint`
- If you get stuck, refer back to slides 4 and 5 of the previous video. We do a similar set of steps there.

`@pre_exercise_code`

```{python}
from urllib.request import urlretrieve

# Load the path for the two datasets
customer_demographics = 'https://assets.datacamp.com/production/repositories/1646/datasets/c3a701a4729471ae0b92d8c300b470fd2ec0a73a/user_demographics_v1.csv'
urlretrieve(customer_demographics, 'customer_data.csv')

purchase_data = 'https://assets.datacamp.com/production/repositories/1646/datasets/5decd183ef3710475958bbc903160fd6354379d5/purchase_data_v1.csv'
urlretrieve(purchase_data, 'inapp_purchases.csv')
```

`@sample_code`
```{python}
# Import pandas 
____

# load the customer_data
customer_data = pd.read_csv(____)

# load the app_purchases
app_purchases = pd.____

# show the head of customer_data
print(customer_data.____)
```

`@solution`
```{python}
# Import pandas 
import pandas as pd 

# load the customer_data
customer_data = pd.read_csv('customer_data.csv')

# load the app_purchases
app_purchases = pd.read_csv('inapp_purchases.csv')

# show the head of customer_data
print(customer_data.head())
```

`@sct`
```{python}
success_msg("Great start!")
```


---
## Merging on Different Sets of Fields. 

```yaml
type: BulletExercise
key: c466977e85
lang: python
xp: 100
```
In this exercise we will explore merging on different parameters and look at how this impacts our final results. Our two datasets from the 
previous exercise have been loaded for us.

`@pre_exercise_code`
```{python}
from urllib.request import urlretrieve
import pandas as pd

# Load the path for the two datasets
customer_demographics = 'https://assets.datacamp.com/production/repositories/1646/datasets/c3a701a4729471ae0b92d8c300b470fd2ec0a73a/user_demographics_v1.csv'
urlretrieve(customer_demographics, 'customer_data.csv')

purchase_data = 'https://assets.datacamp.com/production/repositories/1646/datasets/5decd183ef3710475958bbc903160fd6354379d5/purchase_data_v1.csv'
urlretrieve(purchase_data, 'inapp_purchases.csv')

# Load the dataframes
# load the customer_data
customer_data = pd.read_csv('customer_data.csv')
customer_data = customer_data.rename(index=str, columns={"reg_date": "date"})
customer_data.date = pd.to_datetime(customer_data.date)


# load the app_purchases
app_purchases = pd.read_csv('inapp_purchases.csv')
app_purchases.date = pd.to_datetime(app_purchases.date)
```

`@sample_code`
```{python}
# Merge on the 'uid' field
uid_combined_data = ____.merge(____, on=____, how='inner')

# Examine the results 
print(uid_combined_data.head())
print(len(uid_combined_data))
```

***

### Joining on UID
```yaml
type: NormalExercise
xp: 50
key: ccbaba969d
```

`@instructions`
- Merge the demographics data onto the purchase data, combining on the `uid` field. 

`@hint`
Remember to pass in the values to the `on` argument as a list. 

`@solution`
```{python}
# Merge on the 'uid' field
uid_combined_data = app_purchases.merge(customer_data, on=['uid'], how='inner')

# Examine the results 
print(uid_combined_data.head())
print(len(uid_combined_data))
```

`@sct`
```{python}
success_msg("Great!")
```

***

### Merging by UID and Date

```yaml
type: NormalExercise
xp: 50
key: a6bb80f85f
```

`@instructions`
- Now to look at purchases that happend **on** the date of registration join on `uid` and `date` in our two datasets.

`@hint`
- The `reg_date` column in `customer_data` has been renamed to `date`

`@sample_code`
```{python}
# Merge on the 'uid' field
uid_date_combined_data  = ____.merge(____, on=____, how='inner')

# Examine the results 
print(uid_date_combined_data.head())
print(len(uid_date_combined_data))
```

`@solution`
```{python}
# Merge on the 'uid' field
uid_date_combined_data = app_purchases.merge(customer_data, on=['uid', 'date'], how='inner')

# Examine the results 
print(uid_date_combined_data.head())
print(len(uid_date_combined_data))
```

`@sct`
```{python}
success_msg("Awesome Job, note how many fewer rows our result this time has returned than previously!")
```
---
## Tools for the Exploratory Analysis of KPIs

```yaml
type: VideoExercise
lang: python
xp: 50
skills: 2
key: 602157fec2
```

Here, we will bring together everything we have learned so far to apply the `.groupby()` and `.agg()` methods to calculate some important conversion rate KPIs across different groups of our dataset. Then we will finish off this chapter with a discussion of how to determine KPIs in a general business or research setting. 


`@video_link`

//player.vimeo.com/video/154783078

`@video_hls`

//videos.datacamp.com/transcoded/000_placeholders/v1/hls-temp.master.m3u8

`@projector_key`
8c48eee703f333a590fe5135979c6860


---
## Practicing Aggregations

```yaml
type: BulletExercise
key: 3c2c2b468a
lang: python
xp: 100
```
In this exercise, we will begin exploring our in app purchase data in a more considered manner. Loaded for you is a dataFrame named `purchase_data` which is our dataset of in-app purchase data merged with user demographics from earlier. We will practice aggregating the dataset in various ways using the `agg` method and examining our results to get an understanding of the overall data. 


`@pre_exercise_code`
```{python}
from urllib.request import urlretrieve
import pandas as pd

# Load the path for the two datasets
customer_demographics = 'https://assets.datacamp.com/production/repositories/1646/datasets/c3a701a4729471ae0b92d8c300b470fd2ec0a73a/user_demographics_v1.csv'
urlretrieve(customer_demographics, 'customer_data.csv')

purchase_data = 'https://assets.datacamp.com/production/repositories/1646/datasets/5decd183ef3710475958bbc903160fd6354379d5/purchase_data_v1.csv'
urlretrieve(purchase_data, 'inapp_purchases.csv')

app_purchases = pd.read_csv('inapp_purchases.csv')
customer_demographics = pd.read_csv('customer_data.csv')
purchase_data = app_purchases.merge(customer_demographics, how='inner', on=['uid'])
```

`@sample_code`
```{python}
# Caculate the mean purchase price 
purchase_price_mean = purchase_data.____.agg(____)

# Examine the output 
print(purchase_price_mean)
```

***

### Mean Purchase Price

```yaml
type: NormalExercise
xp: 30
key: '5985691225'
```

`@instructions`
First, find the `mean` purchase price paid across our dataset. Then examine the output before moving on. 

`@hint`
Remember, built in functions like `.mean()` need to be in quotations when passed to the `.agg()` method. 

`@solution`
```{python}
# Caculate the mean purchase price 
purchase_price_mean = purchase_data.price.agg('mean')

# Examine the output 
print(purchase_price_mean)
```

`@sct`
```{python}
success_msg("Great work! Lets expand on this method!")
```

***

### Mean and Median Purchase Price 

```yaml
type: NormalExercise
xp: 30
key: 1bc50fd4a5
```

`@instructions`
Now, use the `agg()` method to find the `mean` and `median` together. 

`@hint`
Remember, we can pass multiple arguments to `.agg()` in the form of a list.

`@sample_code`
```{python}
# Caculate the mean purchase price 
purchase_price_summary = purchase_data.____.agg(____)

# Examine the output 
print(purchase_price_summary)
```


`@solution`
```{python}
# Caculate the mean purchase price 
purchase_price_summary = purchase_data.price.agg(['mean', 'median'])

# Examine the output 
print(purchase_price_summary)
```

`@sct`
```{python}
success_msg("Awesome Job!")
```

***

### Summarizing Multiple Fields
```yaml
type: NormalExercise
xp: 40
key: 9e42b4aa21
```

`@instructions`
Now, find the `mean` and `median` for both the price paid and the age of purchaser.

`@hint`
Remember, to summarize multiple fields, we can pass them in as the keys of a dictionary.

`@sample_code`
```{python}
# Caculate the mean purchase price 
purchase_summary = purchase_data.agg(____)

# Examine the output 
print(purchase_summary)
```


`@solution`
```{python}
# Caculate the mean purchase price 
purchase_summary = purchase_data.agg({'price': ['mean', 'median'], 'age': ['mean', 'median']})

# Examine the output 
print(purchase_summary)
```

`@sct`
```{python}
success_msg("Incredible, Congratulations!")
```

---
## Grouping & Aggregating

```yaml
type: NormalExercise
key: d93fd484af
lang: python
xp: 100
skills: 2
```

In this exercise, we will combine what we have learned about aggregation and grouping to calculate a set of summary statistics about our purchase data broken out by device, and gender. We will then compare the values across these subsets. This  will give us a baseline for these values as potential KPIs to optimize going forward. The `purchase_data` dataset, containing purchases merged with user demographics has been preloaded for you.  

`@instructions`
- Group the `purchase_data` dataFrame by country and gender. 
- Aggregate the data, finding the mean, median, and standard deviation of the purchase price across these groups. 
- Examine the results, does the mean differ drastically from the median? How much variability is in each group? 

`@hint`
The built in standard deviation method in python is `.std()`

`@pre_exercise_code`
```{python}
from urllib.request import urlretrieve
import pandas as pd

# Load the path for the two datasets
customer_demographics = 'https://assets.datacamp.com/production/repositories/1646/datasets/c3a701a4729471ae0b92d8c300b470fd2ec0a73a/user_demographics_v1.csv'
urlretrieve(customer_demographics, 'customer_data.csv')

purchase_data = 'https://assets.datacamp.com/production/repositories/1646/datasets/5decd183ef3710475958bbc903160fd6354379d5/purchase_data_v1.csv'
urlretrieve(purchase_data, 'inapp_purchases.csv')

app_purchases = pd.read_csv('inapp_purchases.csv')
customer_demographics = pd.read_csv('customer_data.csv')
purchase_data = app_purchases.merge(customer_demographics, how='inner', on=['uid'])
```

`@sample_code`
```{python}
# Group the data 
grouped_purchase_data = purchase_data.____

# Aggregate the Data
purchase_summary = grouped_purchase_data.____(____)

# Examine the results
print(purchase_summary)
```

`@solution`
```{python}
# Group the data 
grouped_purchase_data = purchase_data.groupby(by=['device', 'gender'])

# Aggregate the Data
purchase_summary = grouped_purchase_data.agg({'price': ['mean', 'median', 'std']})

# Examine the results
print(purchase_summary)
```

`@sct`
```{python}
success_msg("Awesome, This gives a great sense of the baselines for these groups!")
```
---
## Calculating KPIs - A Practical Example

```yaml
type: VideoExercise
key: b834985e6a
lang: python
xp: 50
skills: 2
```
In our final lesson of this chapter we leverage everything we learned in our first three lessons to calculate the conversion rate for our example dataset. We will walk through the code and thought process behind calculating this KPI before examining it across various subsets of our user base. To conclude we will discuss some heuristics for choosing a good KPI for your particular circumstances. 

`@video_link`

//player.vimeo.com/video/154783078

`@video_hls`

//videos.datacamp.com/transcoded/000_placeholders/v1/hls-temp.master.m3u8

`@projector_key`
6f1a3e5c8bc13df93939396d0b657e3c







---
## Calculating KPIs

```yaml
type: NormalExercise
key: aa048f1dc2
lang: python
xp: 100
skills: 2
```
Now let us take what we have learned and work through calculating a KPI ourselves. Using our `purchase_data` dataFrame from before, calculate the average amount paid per purchase within a users first 28 days. This KPI can provide a sense of the popularity of different in-app purchase
price points to users within their first month. 

`@instructions`
- Using our `purchase_data` dataFrame, filter out all users who registered in the last 28 days. The `current_date` variable has already been defined.
- Next, filter this dataset to only include purchases within the last 28 days. 
- Finally, find the average of the price paid on purchases in this dataFrame. 



`@hint`
Recall that we can filter a dataFrame by providing a boolean operation as an index as we did in the video exercise. 


`@pre_exercise_code`
```{python}
from urllib.request import urlretrieve
import pandas as pd
from datetime import datetime, timedelta

# Load the path for the two datasets
customer_demographics = 'https://assets.datacamp.com/production/repositories/1646/datasets/c3a701a4729471ae0b92d8c300b470fd2ec0a73a/user_demographics_v1.csv'
urlretrieve(customer_demographics, 'customer_data.csv')

purchase_data = 'https://assets.datacamp.com/production/repositories/1646/datasets/5decd183ef3710475958bbc903160fd6354379d5/purchase_data_v1.csv'
urlretrieve(purchase_data, 'inapp_purchases.csv')

app_purchases = pd.read_csv('inapp_purchases.csv')
customer_demographics = pd.read_csv('customer_data.csv')
purchase_data = app_purchases.merge(customer_demographics, how='inner', on=['uid'])
purchase_data.reg_date = pd.to_datetime(purchase_data.reg_date)
purchase_data.date = pd.to_datetime(purchase_data.date)

# The current date for our purposes
current_date = pd.to_datetime('2018-03-17')
```

`@sample_code`
```{python}
# Find the last date in our dataset we will count purchases from 
max_purchase_date = ____ - timedelta(days=____)

# Filter to only include users who registered on or before our max date
purchase_data_filt = purchase_data[____ < ____]

# Filter to contain only Purchases within the first 28 days of registration
purchase_data_filt = ____[(____ <= 
                        purchase_data_filt.reg_date + ____)]
                     
# Output the mean price paid per purchase
print(purchase_data_filt.____.____)
```

`@solution`
```{python}
# Find the last date in our dataset we will count purchases from 
max_purchase_date = current_date - timedelta(days=28)

# Filter to only include users who registered on or before our max date
purchase_data_filt = purchase_data[purchase_data.reg_date < max_purchase_date]

# Now filter to contain purchaes within the first 28 days of registration
purchase_data_filt = purchase_data_filt[(purchase_data_filt.date <= 
                        purchase_data_filt.reg_date + timedelta(days=28))]
                     
# Output the mean price paid per purchase
print(purchase_data_filt.price.mean())
```

`@sct`
```{python}
success_msg("Awesome! It seems like our $4.99 and slightly lower price points are popular.")
```



---
## Measuring the Average Purchase Price By Cohort

```yaml
type: TabExercise
key: 9337c0defc
lang: python
xp: 100
```

Building on the previous exercise, lets look at the same KPI, average purchase price, and a similar one, median purchase price, within the first 28 days. Additionally lets look at these metrics not limited to 28 days to compare. 

We can calculate these metrics across a set of cohorts and see what differences emerge. this is a useful task as it can help us understand how behaviors vary across cohorts. 


`@pre_exercise_code`
```{python}
from urllib.request import urlretrieve
import pandas as pd
import numpy as np
from datetime import datetime, timedelta

# Load the path for the two datasets
customer_demographics = 'https://assets.datacamp.com/production/repositories/1646/datasets/c3a701a4729471ae0b92d8c300b470fd2ec0a73a/user_demographics_v1.csv'
urlretrieve(customer_demographics, 'customer_data.csv')

purchase_data = 'https://assets.datacamp.com/production/repositories/1646/datasets/5decd183ef3710475958bbc903160fd6354379d5/purchase_data_v1.csv'
urlretrieve(purchase_data, 'inapp_purchases.csv')

app_purchases = pd.read_csv('inapp_purchases.csv')
customer_demographics = pd.read_csv('customer_data.csv')
purchase_data = app_purchases.merge(customer_demographics, how='inner', on=['uid'])
purchase_data.reg_date = pd.to_datetime(purchase_data.reg_date)
purchase_data.date = pd.to_datetime(purchase_data.date)

current_date = pd.to_datetime('2018-03-17')
```

***

### Add Calculation columns 

```yaml
type: NormalExercise
xp: 30
key: fa81a8d856
```

`@instructions`
 - To set up our `purchase_data` for aggregation add a variable `month1` that is `np.NaN` for values that do not fit our two date conditions from last exercise and the purchase price for those that do. The `current_date` has been loaded.

`@sample_code`
```{python}
# Find the max purchase date allowable
max_purchase_date = current_date - ____

# Find the Month 1 Values 
month1 = np.where((____ <= ____) &
                 (____ <= ____ + ____)
                 , ____, None)
                 
# Update the value in the dataFrame
purchase_data[____] = ____
```

`@solution`
```{python}
# Find the max purchase date allowable
max_purchase_date = current_date - timedelta(days=28)

# Find the Month 1 Values 
month1 = np.where((purchase_data.reg_date < max_purchase_date) &
                 (purchase_data.date <= purchase_data.reg_date + timedelta(days=28)),
                 purchase_data.price, np.NaN)
                 
# Update the value in the dataFrame 
purchase_data['month1'] = month1
```

`@hint`
The two date conditions are (1) the user having been registerd prior to the most recent 28 days and (2) the purchase having come within 28 days of registration.

`@sct`
```{python}
success_msg("Not only do intermediate calculations help for aggregation, they are great for catching errors.")
```

***

### Grouping the Data

```yaml
type: NormalExercise
xp: 30
key: 4a4c0f8dbe
```

`@instructions`
- Now, group our dataFrame by `gender` and `device`. 


`@sample_code`
```{python}
# Find the max purchase date allowable
max_purchase_date = current_date - timedelta(days=28)

# Find the Month 1 Values 
month1 = np.where((purchase_data.reg_date < max_purchase_date) &
                 (purchase_data.date <= purchase_data.reg_date + timedelta(days=28)),
                 purchase_data.price, np.NaN)
                 
# Update the value in the dataFrame 
purchase_data['month1'] = month1

# Group the data by gender and device 
purchase_data_upd = purchase_data.(____, ____) 
```

`@solution`
```{python}
# Find the max purchase date allowable
max_purchase_date = current_date - timedelta(days=28)

# Find the Month 1 Values 
month1 = np.where((purchase_data.reg_date < max_purchase_date) &
                 (purchase_data.date <= purchase_data.reg_date + timedelta(days=28)),
                 purchase_data.price, np.NaN)
                 
# Update the value in the dataFrame 
purchase_data['month1'] = month1

# Group the data by gender and device 
purchase_data_upd = purchase_data.groupby(by=['gender', 'device'], as_index=False) 
```


`@hint`
Don't forget about the `as_index` parameter! 

`@sct`
```{python}
success_msg("Fantastic! Now on to the final part!")
```

***

### Aggregating the Data

```yaml
type: NormalExercise
xp: 40
key: f0107bd270
```


`@instructions`
- Now find the mean and median price paid in the first month broken out by gender and device.
- Add code to examine the mean and median price paid overall for users. 

`@sample_code`
```{python}
# Find the max purchase date allowable
max_purchase_date = current_date - timedelta(days=28)

# Find the Month 1 Values 
month1 = np.where((purchase_data.reg_date < max_purchase_date) &
                 (purchase_data.date <= purchase_data.reg_date + timedelta(days=28)),
                 purchase_data.price, np.NaN)
                 
# Update the value in the dataFrame 
purchase_data['month1'] = month1

# Group the data by gender and device 
purchase_data_upd = purchase_data.groupby(by=['gender', 'device'], as_index=False) 

# Aggregate the month1 and price data 
purchase_summary = purchase_data_upd.agg(____)

# Examine the results 
print(purchase_summary)
```

`@solution`
```{python}
# Find the max purchase date allowable
max_purchase_date = current_date - timedelta(days=28)

# Find the Month 1 Values 
month1 = np.where((purchase_data.reg_date < max_purchase_date) &
                 (purchase_data.date <= purchase_data.reg_date + timedelta(days=28)),
                 purchase_data.price, np.NaN)
                 
# Update the value in the dataFrame 
purchase_data['month1'] = month1

# Group the data by gender and device 
purchase_data_upd = purchase_data.groupby(by=['gender', 'device'], as_index=False) 

# Aggregate the month1 and price data 
purchase_summary = purchase_data_upd.agg(
                        {'month1': ['mean', 'median'],
                        'price': ['mean', 'median']})

# Examine the results 
print(purchase_summary)
```

`@hint`
Remember the arguments must be passed in as a dictionary when calling the method on this number of fields. 

`@sct`
```{python}
success_msg("Great! This value seems relatively stable past 28 days.")
```
