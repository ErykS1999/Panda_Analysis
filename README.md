## The first thing is to load in the data. In this analysis, I will focus on the first five rows. data.head() allows us to do so:

```
import numpy as np
import pandas as pd

data = pd.read_csv('airbnb/Airbnb_Open_Data.csv')

data.shape

data.head()
```

## In order to continue working on cleaning the data, I had to rename the columns to make the readability more clear.

```
data.rename(columns={'NAME':'airbnb name','number of reviews':'reviews_sum','calculated host listings count':'host listings',
                     'house_rules':'rules','minimum nights':'min_nights','host_identity_verified':'host_verify','neighbourhood group':'area'})


```

## We had to analyse which rows have diplicated values as well as find out any values that are empty:

```
data.head().isnull().sum()

data.head().duplicated().sum()
```

## After finding out that host_identity_verified has empty values, we had to highlight that column in order to work on in it. 

```
data[['host_identity_verified']].head()

```

## Changing the values from lower to upper case will adapt the text to be the same throughout the table. 

```
data['host_identity_verified'].replace({'unconfirmed':'Unverified'}, inplace=True)


# Don't forget to make the capital letters of all 'verified' rows

data.replace({'verified':'Verified'}, inplace=True)

data.head()

```

## .loc allows the text to select the specific value in the table. iloc allows us to use indexing to select the specific value.

```
data.loc[data['NAME'] == 'Skylit Midtown Castle', 'license'] = data.loc[data['NAME'] == 'Skylit Midtown Castle', 'license'].replace({'unconfirmed':'Success'})


data.head()

```

## The below code, showcases thinking ahead with .map and lambda x. For future references, if someome writes unconfirmed in the reviews per month column, the data will automatically change to 'NEEDS ATTENTION'.

```
data['reviews per month'] = data['reviews per month'].map(lambda x: 'NEEDS ATTENTION!' if x == 'unconfirmed' else x)

data.head()

```

## First time creating a bar graph in python using .plot. This presents the data in a clear and visible way.

```
ax = data['neighbourhood group'].value_counts().head(10).plot(kind='bar',title='Airbnbs in each city')

ax.set_xlabel('City')
ax.set_ylabel('Number of Airbnbs')

```


## After creating two bar charts, I have created a screen recording of the whole presentation of the jupyter document: 



https://github.com/user-attachments/assets/ca3d9cd0-dc91-409a-bdb8-df0d1aedf41d


