# predicting-risk-of-eviction
## predicting risk of eviction and understanding the factors that increase that risk
### Summary
The culminating task for the Microsoft Professional Program in Data Science was to use the tools for predicting risk of eviction and understanding the factors that increase that risk. Digging into underlying patterns in evictions data can be an important first step toward greater visibility and better policies. Our goal is to predict the number of evictions at the county level from other socioeconomic and demographic indicators. According to the Eviction Lab, "An eviction happens when a landlord expels people from property he or she owns. Evictions are landlord-initiated involuntary moves that happen to renters." The data is compiled from a wide range of sources and made publicly available by the United States Department of Agriculture Economic Research Service and the Eviction Lab. This report will review data exploration that was done to examine the relationship between features that were available in the data using descriptive statstics and data visualization. These finding lead us to know what to exclude from the model as well as suggested what would likely help us identify the number of evictions.
### Exploring The Data
Features
There are 47 variables in this dataset. Each row in the dataset represents a United States county, and the dataset we are working with covers two particular years, denoted a, and b. We provide a unique identifier for an individual county, but note that the counties in the test set are distinct from counties in the train set. In other words, no county that appears in the train set will appear in the test set. Thus, county-specific features (i.e. county dummy variables) will not be an option. However, the counties in the test set still share similar patterns as those in the train set and so other feature engineering will work the same as usual.

ID
county_code :  Unique identifier for each county
year : Year, denoted as a or b
state : Unique identifier for each state
population : Total population
HOUSING
renter_occupied_households : Count of renter-occupied households
pct_renter_occupied : Percent of occupied housing units that are renter-occupied
median_gross_rent : Median cost of rent
median_household_income : Median household income
median_property_value : Median property value
rent_burden : Median gross rent as a percentage of household income
ETHNICITY
pct_white : Percent of population that is White alone and not Hispanic or Latino
pct_af_am : Percent of population that is Black or African American alone and not Hispanic or Latino
pct_hispanic : Percent of population that is of Hispanic or Latino origin
pct_am_ind : Percent of population that is American Indian and Alaska Native alone and not Hispanic or Latino
pct_asian : Percent of population that is Asian alone and not Hispanic or Latino
pct_nh_pi : Percent of population that is Native Hawaiian and Other Pacific Islander alone and not Hispanic or Latino
pct_multiple : Percent of population that is two or more races and not Hispanic or Latino
pct_other : Percent of population that is other race alone and not Hispanic or Latino
ECONOMIC
poverty_rate : Percent of the population with income in the past 12 months below the poverty level
rucc : Rural-Urban Continuum Codes "form a classification scheme that distinguishes metropolitan counties by the population size of their metro area, and nonmetropolitan counties by degree of urbanization and adjacency to a metro area. The official Office of Management and Budget (OMB) metro and nonmetro categories have been subdivided into three metro and six nonmetro categories. Each county in the U.S. is assigned one of the 9 codes." (USDA Economic Research Service)
urban_influence : Urban Influence Codes "form a classification scheme that distinguishes metropolitan counties by population size of their metro area, and nonmetropolitan counties by size of the largest city or town and proximity to metro and micropolitan areas." (USDA Economic Research Service)
economic_typology : County Typology Codes "classify all U.S. counties according to six mutually exclusive categories of economic dependence and six overlapping categories of policy-relevant themes. The economic dependence types include farming, mining, manufacturing, Federal/State government, recreation, and nonspecialized counties. The policy-relevant types include low education, low employment, persistent poverty, persistent child poverty, population loss, and retirement destination." (USDA Economic Research Service)
pct_civilian_labor : Civilian labor force, annual average, as percent of population.
pct_unemployment : Unemployment, annual average, as percent of population
HEALTH
pct_uninsured_adults : Percent of adults without health insurance
pct_uninsured_children : Percent of children without health insurance
pct_adult_obesity : Percent of adults who meet clinical definition of obese
pct_adult_smoking : Percent of adults who smoke
pct_diabetes : Percent of population with diabetes
pct_low_birthweight : Percent of babies born with low birth weight
pct_excessive_drinking : Percent of adult population that engages in excessive consumption of alcohol
pct_physical_inactivity : Percent of adult population that is physically inactive
air_pollution_particulate_matter_value : Fine particulate matter in µg/m³
homicides_per_100k : Deaths by homicide per 100,000 population
motor_vehicle_crash_deaths_per_100k : Deaths by motor vehicle crash per 100,000 population
heart_disease_mortality_per_100k : Deaths from heart disease per 100,000 population
pop_per_dentist : Population per dentist
pop_per_primary_care_physician : Population per Primary Care Physician
DEMOGRAPHIC
pct_female : Percent of population that is female
pct_below_18_years_of_age : Percent of population that is below 18 years of age
pct_aged_65_years_and_older : Percent of population that is aged 65 years or older
pct_adults_less_than_a_high_school_diploma : Percent of adult population that does not have a high school diploma
pct_adults_with_high_school_diploma : Percent of adult population which has a high school diploma as highest level of   education achieved
pct_adults_with_some_college : Percent of adult population which has some college as highest level of education achieved
pct_adults_bachelors_or_higher : Percent of adult population which has a bachelor's degree or higher as highest level of education achieved
birth_rate_per_1k : Births per 1,000 of population
death_rate_per_1k : Deaths per 1,000 of population

### Choosing the Model
I trained 4 different models and GradientBoostingRegressor shows the best result.

Fitting completed in: 459.3602931499481 GradientBoostingRegressor(alpha=0.9, criterion='mse', init=None, learning_rate=0.05, loss='ls', max_depth=5, max_features=None, max_leaf_nodes=None, min_impurity_split=1e-07, min_samples_leaf=1, min_samples_split=3, min_weight_fraction_leaf=0.0, n_estimators=500, presort='auto', random_state=None, subsample=1.0, verbose=0, warm_start=False) MSE on train data: 13.7866 MRSE on train data: 3.71304 Score on train data: 96.8697348716 %

So we got a score of 96.86 on our test data.

### Conclusion
As we can see from the analysis has demonstrated the relationships between number of evictions and several features affecting this matter. In particular, the analysis shows that regional variance play significant roles the model, which indicates that demographical distribution of customers are very important. In addition, different models absorb different sets of parameters to evaluate. While median household income, median gross rent, poverty rate and urban influence are the most important features for the model, diabetes and uninsured adults are not as important when determining thenumber of evictions.

### What's next
Suppose that this report represented an exploratory pilot of the eviction problem and that the governent is sufficiently convinced that the problem is modelable. What would be our next steps?

A first step would definitely be to invest in data collection. So we would want to source or collect more data and build up a larger database. Some of the features would need changing as well. Geographic data seems really important in this model, and yet we weren’t given absolute measurements of location. Something like lat/long would be more generalizable. Finally, we would want to make some determination about our needs from the model. Determinations like how accurate do we need the model to be to be confident in our decision making? Do we care about predicting one class over the others?
