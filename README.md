## Problem Statement

In order to be able to more accurately determine which communities will be hit hardest in a future pandemic, we set out to use covid-related statistics to predict poverty and death rates in counties across United States. If we can establish a good model then we can identify different idicators of Covid death rates, which can then in turn help look for issues within counties and states to increase health care and accessibility.

## Table of Contents

1. [Executive Summary](#executive-summary)
2. [Data Cleaning](#data-cleaning)
3. [Exploratory Data Analysis](#exploratory-data-analysis)
4. [Modeling](#modeling)
5. [Results & Conclusions](#results-and-conclusions)
7. [Data Dictionary](#data-dictionary)

## Executive Summary


COVID-19 is caused by a coronavirus called SARS-CoV-2. Older adults and people who have severe underlying medical conditions like heart or lung disease or diabetes seem to be at higher risk for developing more serious complications from COVID-19 illness.

This once in a lifetime global health crisis resulted in large loss of life (3,786,968 deaths of people worldwide at the time this is being written, and 599,510 deaths in the United States). Our analysis sets out to predict the death rate depending upon various demographic factors contained within the US Census and New York Times COVID-19 datasets. We suspected that lower income communities would be more greatly impacted by COVID-19, so we also wanted to use poverty rate as a target for another set of models in order to determine the features that are most indicative of poverty rate.



## Data Cleaning

### Imports required

see `environment.yaml`

### Datasets:

- Covid19 death rates per US county (covid = covid19_nyt_us_counties.csv)
- Census bureau acs per county (census = census_bureau_acs_county_2018_5yr.csv)
- US Healthcare Capacity per county (healthcare = us_healthcare_capacity-county-CovidCareMap.csv)


### Primary goals:

- drop columns with more than 100 null values
- impute mean for columns used in modelling
- keep as many rows as possible


## Exploratory Data Analysis

- We used 'all bed occupancy rate' from the healthcare dataset in our models so we imputed the mean and all other rows from this dataset were dropped due to high collinearity
- Grouped covid data by fips code to give us the most recent covid information for each county which was from 6/3
- Create variables for `death_rate`, `poverty_rate`
- Visualized heatmap correlations
- Added leading zeros to county fips codes for use in choropleth maps


## Modeling

### For poverty_rate:
**Feature Selection:**

We Selecting features was difficult when predicting poverty rates. Most of the features in the census data were directly related to poverty rate in some way. Including them could lead to data leakage. For instance the `worked_from_home` feature is related to poverty rate because the jobs you can do from home are going to inherently be higher paying. Low wage jobs typically can't be done from home. We ended up using mostly demographic data about race and households. The model that performed the best was a random forest regressor.

**Trouble Ahead, Trouble Behind:**

Due to the demographic features selected, this initial investigation into predicting poverty rates turned into more of an exposé of systemic racism in america. While the results are interesting they do not support our goal of determining which communites have a high chance of being adversly affected by future pandemics. Because of this we decided to use census data to predict death rates instead.

### For death_rate:
- Scaled X and y using StandardScaler
- Multiple initial models: Linear Regression, Random Forest Regressor, Ada Boost Regressor, Gradient Boosting Regressor, Voting Regressor
- Selected Model: Random Forest Regressor
- Features: top 20 feature importances
- Make death rate predictions, plot against actual values



## Results and Conclusions


**Voting Regressor using feature importances:**

- Cross Val Score 0.3596772082727179 +/- 0.04760577126862348
- Test Score:  0.3642262108365024
- Baseline RMSE:  0.00893
- Model RMSE:     0.00712
- Improvement:    0.00181

**Conclusions**

Poverty rates and covid death rates are closely intertwined. Features such as the percent of population living in low income housing stood out as the most important factors for our models when predicting death rates. This might be due to the difficulty in accessing healthcare in the U.S.A. Having more money tends to mean having access to quality care. Our project supports the notion that when the next pandemic hits lives can be saved if we allocate funds to poorer communities.

**Next Steps**

- Look at insurance coverage vs death rates
- Look at percent of population working in service industry vs death rates
- Sentiment analysis of political ideations in higher death rate communities
- Look at top news outlets in communities vs death rate
