## Problem Statement

In order to be able to more accurately determine which communities will be hit hardest in a future pandemic, we set out to use covid-related statistics to predict poverty and death rates in counties across United States. If we can establish a good model then we can infer that Covid rates differ by poverty, which can then in turn help look for issues within counties and states to increase health care and accessibility.

## Table of Contents

1. [Executive Summary](#executive-summary)
2. [Data Cleaning](#data-cleaning)
3. [Exploratory Data Analysis](#exploratory-data-analysis)
4. [Modeling](#modeling)
5. [Results & Conclusions](#results-&-conclusions)
6. [Data Dictionary](#data-dictionary)

## Executive Summary


COVID-19 is caused by a coronavirus called SARS-CoV-2. Older adults and people who have severe underlying medical conditions like heart or lung disease or diabetes seem to be at higher risk for developing more serious complications from COVID-19 illness.

This once in a lifetime global health crisis resulted in large loss of life (3,786,968 deaths of people worldwide at the time this is being written, and 599,510 deaths in the United States). Our analysis sets out to predict the death rate depending upon various demographic factors contained within the US Census and New York Times COVID-19 datasets. We suspected that lower income communities would be more greatly impacted by COVID-19, so we also wanted to use poverty rate as a target for another set of models in order to determine the features that are most indicative of poverty rate.



## Data Cleaning

### Imports required:

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

- We will use all hospital bed occupancy rate in our models so we impute the mean and all other rows are dropped
- Group covid data by fips code to give us the most recent covid information for each county which is from 6/3
- Create variables for `death_rate`, `poverty_rate`
- Visualize heatmap correlations
- Add leading zeros to county fips codes for use in choropleth maps


## Modeling

### For death_rate:

- Scale X and y
- Random Forest Regressor
- Features: top 20 feature importances
- Make death rate predictions, plot against actual values

### For poverty_rate:
**Feature Selection**
  Selecting features was difficult when predicting poverty rates. Most of the features in the census data were related directly to poverty rate in some way. For instance the `worked_from_home` feature is correlated with poverty rate because the jobs you can do from home are going to inherently be higher paying. Low wage jobs typically can't be done from home.
  

## Results & Conclusions

### For death_rate:

*Random Forest Regressor using feature importances:*

- Best Score:  0.36030836413930434
- Cross Val Score 0.36030836413930434 +/- 0.0684718488109917
- Test Score:  0.3624652029664446
- Baseline RMSE: .00778

*Conclusions*

Since the plotted residuals are close to normally distributed, we can infer that the features used in this model are good predictors of death rate. For real world application, we can see that it is important to provide assistance to people living in close quarters and people in states of poverty. One can infer that death rate is closely tied to determiners of poverty.

### For poverty_rate:


## Data Dictionary

|Feature|Type|Dataset|Description|
|---|---|---|---|
|**unemployment_rate**|*float*|*final_df* | 'unemployed_pop' divided by total county'population
|**death_rate**|*float*|*final_df* |deaths from covid divided by confirmed cases
|**poverty_rate**|*float*|*final_df* | pop_determined_poverty_status from census divided by total county population
|**date**|*object*|*covid*
|**county**|*object*|*covid*
|**state_name, state**|*object*|*covid, counties*
|**county_fips_code, fips_code**| *float*|*covid, counties*
|**confirmed_cases**| *int*|*covid*
|**deaths**| *float*|*covid*
|**do_date**| *object*|*census*
|**total_pop**| *float*|*census*
|**households**| *float*|*census*
|**male_pop**| *float*|*census*
|**female_pop**| *float*|*census*
|**median_age**| *float*|*census*
|**male_under_5**| *float*|*census*
|**male_5_to_9**| *float*|*census*
|**male_10_to_14**| *float*|*census*
|**male_15_to_17**| *float*|*census*
|**male_18_to_19**| *float*|*census*
|**male_20**| *float*|*census*
|**male_21**| *float*|*census*
|**male_22_to_24**| *float*|*census*
|**male_25_to_29**| *float*|*census*
|**male_30_to_34**| *float*|*census*
|**male_35_to_39**| *float*|*census*
|**male_45_to_49**| *float*|*census*
|**male_50_to_54**| *float*|*census*
|**male_55_to_59**| *float*|*census*
|**male_60_to_61**| *float*|*census*
|**male_62_to_64**| *float*|*census*
|**male_65_to_66**| *float*|*census*
|**male_67_to_69**| *float*|*census*
|**male_70_to_74**| *float*|*census*
|**male_75_to_79**| *float*|*census*
|**male_80_to_84**| *float*|*census*
|**male_85_and_over**| *float*|*census*
|**female_under_5**| *float*|*census*
|**female_5_to_9**| *float*|*census*
|**female_10_to_14**| *float*|*census*
|**female_15_to_17**| *float*|*census*
|**female_18_to_19**| *float*|*census*
|**female_20**| *float*|*census*
|**female_21**| *float*|*census*
|**female_22_to_24**| *float*|*census*
|**female_25_to_29**| *float*|*census*
|**female_30_to_34**| *float*|*census*
|**female_35_to_39**| *float*|*census*
|**female_40_to_44**| *float*|*census*
|**female_45_to_49**| *float*|*census*
|**female_50_to_54**| *float*|*census*
|**female_55_to_59**| *float*|*census*
|**female_60_to_61**| *float*|*census*
|**female_62_to_64**| *float*|*census*
|**female_65_to_66**| *float*|*census*
|**female_67_to_69**| *float*|*census*
|**female_70_to_74**| *float*|*census*
|**female_75_to_79**| *float*|*census*
|**female_80_to_84**| *float*|*census*
|**female_85_and_over**| *float*|*census*
|**white_pop**| *float*|*census*
|**population_1_year_and_over**| *float*|*census*
|**population_3_years_over**| *float*|*census*
|**pop_16_over**| *float*|*census*
|**pop_25_years_over**| *float*|*census*
|**pop_25_64**| *float*|*census*
|**not_us_citizen_pop**| *float*|*census*
|**black_pop**| *float*|*census*
|**asian_pop**| *float*|*census*
|**hispanic_pop**| *float*|*census*
|**amerindian_pop**| *float*|*census*
|**other_race_pop**| *float*|*census*
|**two_or_more_races_pop**| *float*|*census*
|**hispanic_any_race**| *float*|*census*
|**not_hispanic_pop**| *float*|*census*
|**asian_male_45_54**| *float*|*census*
|**asian_male_55_64**| *float*|*census*
|**black_male_45_54**| *float*|*census*
|**black_male_55_64**| *float*|*census*
|**hispanic_male_45_54**| *float*|*census*
|**hispanic_male_55_64**| *float*|*census*
|**white_male_45_54**| *float*|*census*
|**white_male_55_64**| *float*|*census*
|**median_income**| *float*|*census*
|**income_per_capita**| *float*|*census*
|**income_less_10000**| *float*|*census*
|**income_10000_14999**| *float*|*census*
|**income_15000_19999**| *float*|*census*
|**income_20000_24999**| *float*|*census*
|**income_25000_29999**| *float*|*census*
|**income_30000_34999**| *float*|*census*
|**income_35000_39999**| *float*|*census*
|**income_40000_44999**| *float*|*census*
|**income_45000_49999**| *float*|*census*
|**income_50000_59999**| *float*|*census*
|**income_60000_74999**| *float*|*census*
|**income_75000_99999**| *float*|*census*
|**income_100000_124999**| *float*|*census*
|**income_125000_149999**| *float*|*census*
|**income_150000_199999**| *float*|*census*
|**income_200000_or_more**| *float*|*census*
|**pop_determined_poverty_status**| *float*|*census*
|**poverty**| *float*|*census*
|**gini_index**| *float*|*census*
|**housing_units**| *float*|*census*
|**renter_occupied_housing_units_paying_cash_median_gross_rent**| *float*|*census*
|**owner_occupied_housing_units_lower_value_quartile**| *float*|*census*
|**owner_occupied_housing_units_median_value**| *float*|*census*
|**owner_occupied_housing_units_upper_value_quartile**| *float*|*census*
|**occupied_housing_units**| *float*|*census*
|**housing_units_renter_occupied**| *float*|*census*
|**vacant_housing_units**| *float*|*census*
|**vacant_housing_units_for_rent**| *float*|*census*
|**vacant_housing_units_for_sale**| *float*|*census*
|**dwellings_1_units_detached**| *float*|*census*
|**dwellings_1_units_attached**| *float*|*census*
|**dwellings_2_units**| *float*|*census*
|**dwellings_3_to_4_units**| *float*|*census*
|**dwellings_5_to_9_units**| *float*|*census*
|**dwellings_10_to_19_units**| *float*|*census*
|**dwellings_20_to_49_units**| *float*|*census*
|**dwellings_50_or_more_units**| *float*|*census*
|**mobile_homes**| *float*|*census*
|**housing_built_2005_or_later**| *float*|*census*
|**housing_built_2000_to_2004**| *float*|*census*
|**housing_built_1939_or_earlier**| *float*|*census*
|**median_year_structure_built**| *float*|*census*
|**married_households**| *float*|*census*
|**nonfamily_households**| *float*|*census*
|**family_households**| *float*|*census*
|**households_public_asst_or_food_stamps**| *float*|*census*
|**male_male_households**| *float*|*census*
|**female_female_households**| *float*|*census*
|**children**| *float*|*census*
|**children_in_single_female_hh**|*float*|*census* 
|**median_rent**| *float*|*census*
|**percent_income_spent_on_rent**| *float*|*census*
|**rent_burden_not_computed**| *float*|*census*
|**rent_over_50_percent**| *float*|*census*
|**rent_40_to_50_percent**| *float*|*census*
|**rent_35_to_40_percent**| *float*|*census*
|**rent_30_to_35_percent**| *float*|*census*
|**rent_25_to_30_percent**| *float*|*census*
|**rent_20_to_25_percent**| *float*|*census*
|**rent_15_to_20_percent**| *float*|*census*
|**rent_10_to_15_percent**| *float*|*census*
|**rent_under_10_percent**| *float*|*census*
|**owner_occupied_housing_units**| *float*|*census*
|**million_dollar_housing_units**| *float*|*census*
|**mortgaged_housing_units**| *float*|*census*
|**different_house_year_ago_different_city**| *float*|*census*
|**different_house_year_ago_same_city**| *float*|*census*
|**families_with_young_children**| *float*|*census*
|**two_parent_families_with_young_children**| *float*|*census*
|**two_parents_in_labor_force_families_with_young_children**| *float*|*census*
|**two_parents_father_in_labor_force_families_with_young_children**| *float*|*census*
|**two_parents_mother_in_labor_force_families_with_young_children**| *float*|*census*
|**two_parents_not_in_labor_force_families_with_young_children**| *float*|*census*
|**one_parent_families_with_young_children**| *float*|*census*
|**father_one_parent_families_with_young_children**| *float*|*census*
|**father_in_labor_force_one_parent_families_with_young_children**| *float*|*census*
|**commute_less_10_mins**| *float*|*census*
|**commute_10_14_mins**| *float*|*census*
|**commute_15_19_mins**| *float*|*census*
|**commute_20_24_mins**| *float*|*census*
|**commute_25_29_mins**| *float*|*census*
|**commute_30_34_mins**| *float*|*census*
|**commute_35_44_mins**| *float*|*census*
|**commute_60_more_mins**| *float*|*census*
|**commute_45_59_mins**| *float*|*census*
|**commuters_16_over**| *float*|*census*
|**walked_to_work**| *float*|*census*
|**worked_at_home**| *float*|*census*
|**no_car**| *float*|*census*
|**no_cars**| *float*|*census*
|**one_car**| *float*|*census*
|**two_cars**| *float*|*census*
|**three_cars**| *float*|*census*
|**four_more_cars**| *float*|*census*
|**aggregate_travel_time_to_work**| *float*|*census*
|**commuters_by_public_transportation**| *float*|*census*
|**commuters_by_bus**| *float*|*census*
|**commuters_by_car_truck_van**| *float*|*census*
|**commuters_by_carpool**| *float*|*census*
|**commuters_by_subway_or_elevated**| *float*|*census*
|**commuters_drove_alone**| *float*|*census*
|**group_quarters**| *float*|*census*
|**associates_degree**| *float*|*census*
|**bachelors_degree**| *float*|*census*
|**high_school_diploma**| *float*|*census*
|**less_one_year_college**| *float*|*census*
|**masters_degree**| *float*|*census*
|**one_year_more_college**| *float*|*census*
|**less_than_high_school_graduate**| *float*|*census*
|**high_school_including_ged**| *float*|*census*
|**bachelors_degree_2**| *float*|*census*
|**bachelors_degree_or_higher_25_64**| *float*|*census*
|**graduate_professional_degree**| *float*|*census*
|**some_college_and_associates_degree**| *float*|*census*
|**male_45_64_associates_degree**| *float*|*census*
|**male_45_64_bachelors_degree**| *float*|*census*
|**male_45_64_graduate_degree**| *float*|*census*
|**male_45_64_less_than_9_grade**| *float*|*census*
|**male_45_64_grade_9_12**| *float*|*census*
|**male_45_64_high_school**| *float*|*census*
|**male_45_64_some_college**| *float*|*census*
|**male_45_to_64**| *float*|*census*
|**employed_pop**| *float*|*census*
|**unemployed_pop**| *float*|*census*
|**pop_in_labor_force**| *float*|*census*
|**not_in_labor_force**| *float*|*census*
|**workers_16_and_over**| *float*|*census*
|**armed_forces**| *float*|*census*
|**civilian_labor_force**| *float*|*census*
|**employed_agriculture_forestry_fishing_hunting_mining**| *float*|*census*
|**employed_arts_entertainment_recreation_accommodation_food**| *float*|*census*
|**employed_construction**| *float*|*census*
|**employed_education_health_social**| *float*|*census*
|**employed_finance_insurance_real_estate**| *float*|*census*
|**employed_information**| *float*|*census*
|**employed_manufacturing**| *float*|*census*
|**employed_other_services_not_public_admin**| *float*|*census*
|**employed_public_administration**| *float*|*census*
|**employed_retail_trade**| *float*|*census*
|**employed_science_management_admin_waste**| *float*|*census*
|**employed_transportation_warehousing_utilities**| *float*|*census*
|**employed_wholesale_trade**| *float*|*census*
|**occupation_management_arts**| *float*|*census*
|**occupation_natural_resources_construction_maintenance**| *float*|*census*
|**occupation_production_transportation_material**| *float*|*census*
|**occupation_sales_office**| *float*|*census*
|**occupation_services**| *float*|*census*
|**management_business_sci_arts_employed**| *float*|*census*
|**sales_office_employed**| *float*|*census*
|**in_grades_1_to_4**| *float*|*census*
|**in_grades_5_to_8**| *float*|*census*
|**in_grades_9_to_12**| *float*|*census*
|**in_school**| *float*|*census*
|**in_undergrad_college**| *float* | *census*
|**fips_code**|  *object* | *counties* 
|**county_name**| *object* | *counties* 
|**staffed_all_beds**| *float* | *counties* 
|**staffed_icu_beds**| *float* | *counties* 
|**licensed_all_beds**| *float* | *counties* 
|**all_bed_occupancy_rate**| *float* | *counties* 
|**population**| *float* | *counties* 
|**population_(20+)**| *float* | *counties* 
|**population_(65+)**| *float* | *counties* 
|**staffed_all_beds_[per_1000_people]**| *float* | *counties* 
|**staffed_all_beds_[per_1000_adults_(20+)]**| *float* | *counties* 
|**staffed_all_beds_[per_1000_elderly_(65+)]**| *float* | *counties* 
|**staffed_icu_beds_[per_1000_people]**| *float* | *counties* 
|**staffed_icu_beds_[per_1000_adults_(20+)]**| *float* | *counties* 
|**staffed_icu_beds_[per_1000_elderly_(65+)]**| *float* | *counties* 
|**licensed_all_beds_[per_1000_people]**| *float* | *counties* 
|**licensed_all_beds_[per_1000_adults_(20+)]**| *float* | *counties* 
|**licensed_all_beds_[per_1000_elderly_(65+)]**| *float* | *counties* 
|**icu_bed_source**| *object* | *counties* 
