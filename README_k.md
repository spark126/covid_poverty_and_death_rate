### Problem Statement

using death rates/other statistics about covid to predict poverty rates in counties across United States
if we can establish a good model then we can inference that covid rates differed by poverty
can help look for issues within counties and states -> health care and accessibility

### Table of Contents

1. [Background](#background)
2. [Data Cleaning](#data-cleaning)
3. [Exploratory Data Analysis](#exploratory-data-analysis)
4. [Modeling](#modeling)
5. [Analysis](#analysis)
6. [Results & Conclusions](#results-&-conclusions)

### Background

**Covid 19**

huge pandemic, never truly seen before
large loss of life and livelihood
proof of states/governors hiding or manipulating covid data
https://en.wikipedia.org/wiki/New_York_COVID-19_nursing_home_scandal (Better proof later)
https://www.theguardian.com/us-news/2020/dec/04/florida-governor-rob-desantis-covid-investigation-misled-public
Dataset Information

Census Data
Covid Death Rates
US Hospital
Existing Literature/Papers

ICU Bed Capacity & Death Rates
Poverty and Death Rate
Sources:

Imports & Data
Imports

In [55]:
import pandas as pd
import matplotlib.pyplot as plt
Datasets

In [56]:
covid = pd.read_csv('../data/covid19_nyt_us_counties.csv')
census = pd.read_csv('../data/census_bureau_acs_county_2018_5yr.csv')
hosps_county = pd.read_csv('../data/us_healthcare_capacity-county-CovidCareMap.csv')
hosps_facility = pd.read_csv('../data/us_healthcare_capacity-facility-CovidCareMap.csv')

### Data Cleaning
In [ ]:

### Exploratory Data Analysis

|Feature|Type|Dataset|Description|
|---|---|---|---|
|**depr**|*int*|*df, all_df*| boolean classifier for determining subreddit a post belongs to|
|**target**|*int*|*df_tvec, df_cvec*|renamed `depr` for modeling purposes|
|**full_post**|*object*|*df, all_df*|title and selftext combined|
|**stemmed**|*object*|*df, all_df*|`full_post` text stemmed with PorterStemmer|

### Modeling
In [ ]:

### Analysis

### Results & Conclusions
In [ ]:
