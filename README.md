# predicting-risk-of-eviction
predicting risk of eviction and understanding the factors that increase that risk
Final Report
Executive Summary
The culminating task for the Microsoft Professional Program in Data Science was to use the tools for predicting risk of eviction and understanding the factors that increase that risk. Digging into underlying patterns in evictions data can be an important first step toward greater visibility and better policies. Our goal is to predict the number of evictions at the county level from other socioeconomic and demographic indicators. According to the Eviction Lab, "An eviction happens when a landlord expels people from property he or she owns. Evictions are landlord-initiated involuntary moves that happen to renters." The data is compiled from a wide range of sources and made publicly available by the United States Department of Agriculture Economic Research Service and the Eviction Lab. This report will review data exploration that was done to examine the relationship between features that were available in the data using descriptive statstics and data visualization. These finding lead us to know what to exclude from the model as well as suggested what would likely help us identify the number of evictions.

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
Intial Data Exploration
 
The training data set has 2546 rows and 48 columns
As we can see descriptive stats are easily available for numeric variables.
count	mean	std	min	25%	50%	75%	max
population	2546.0	106245.937942	322852.004699	116.000000	10293.500000	23863.000000	67968.750000	5.279852e+06
renter_occupied_households	2546.0	15008.009034	53333.684235	14.000000	1052.000000	2580.500000	8098.750000	8.821010e+05
pct_renter_occupied	2546.0	28.147390	7.940140	7.305000	22.884000	26.866000	32.092750	7.061000e+01
median_gross_rent	2546.0	688.838178	183.722492	336.000000	577.250000	642.000000	750.000000	1.728000e+03
median_household_income	2544.0	46050.601415	11584.627249	19328.000000	38495.500000	44480.000000	51526.000000	1.234520e+05
median_property_value	2544.0	129609.579009	76236.606321	32287.000000	85288.250000	108844.000000	151696.250000	9.049370e+05
rent_burden	2546.0	28.520561	4.453165	9.986000	26.047250	28.780000	31.160500	4.953500e+01
pct_white	2546.0	0.776272	0.201149	0.050935	0.655224	0.855478	0.935331	9.951140e-01
pct_af_am	2546.0	0.089774	0.145550	0.000000	0.005669	0.021864	0.094011	8.589974e-01
pct_hispanic	2546.0	0.090604	0.142274	0.000000	0.018179	0.036060	0.089893	9.362008e-01
pct_am_ind	2546.0	0.012467	0.051406	0.000000	0.000999	0.002387	0.005279	8.013643e-01
pct_asian	2546.0	0.011653	0.024372	0.000000	0.002081	0.004961	0.010626	3.376724e-01
pct_nh_pi	2546.0	0.000645	0.002560	0.000000	0.000000	0.000000	0.000402	9.652725e-02
pct_multiple	2546.0	0.017698	0.016072	0.000000	0.009623	0.014561	0.020696	2.084745e-01
pct_other	2546.0	0.000886	0.001763	0.000000	0.000000	0.000202	0.001102	1.982206e-02
poverty_rate	2546.0	12.369856	5.654476	0.000000	8.386000	11.543000	15.291000	4.473200e+01
pct_civilian_labor	2546.0	0.467689	0.073813	0.213000	0.420250	0.469000	0.515000	1.000000e+00
pct_unemployment	2546.0	0.059423	0.020953	0.019000	0.044000	0.057000	0.071000	1.820000e-01
pct_uninsured_adults	2546.0	0.215909	0.065510	0.051000	0.168000	0.214000	0.259750	4.950000e-01
pct_uninsured_children	2546.0	0.086385	0.040314	0.014000	0.057000	0.077000	0.106000	2.830000e-01
pct_adult_obesity	2546.0	0.306656	0.041930	0.151000	0.285000	0.308000	0.333000	4.710000e-01
pct_adult_smoking	2138.0	0.214645	0.060863	0.046000	0.174000	0.211000	0.250000	5.110000e-01
pct_diabetes	2546.0	0.109647	0.022321	0.041000	0.094000	0.109000	0.123000	1.980000e-01
pct_low_birthweight	2420.0	0.084065	0.021438	0.040000	0.070000	0.080000	0.091000	2.310000e-01
pct_excessive_drinking	1736.0	0.163274	0.050181	0.042000	0.127000	0.163000	0.196000	3.090000e-01
pct_physical_inactivity	2546.0	0.276156	0.052099	0.120000	0.243000	0.278000	0.310000	4.410000e-01
air_pollution_particulate_matter_value	2545.0	11.703125	1.551625	7.542542	10.501742	12.016457	12.971126	1.488095e+01
homicides_per_100k	948.0	5.847500	5.057310	-0.400000	2.597500	4.500000	7.900000	5.049000e+01
motor_vehicle_crash_deaths_per_100k	2238.0	20.922766	10.134145	3.090000	13.440000	19.500000	26.377500	7.605000e+01
heart_disease_mortality_per_100k	2546.0	279.705813	57.150849	109.000000	239.000000	276.000000	316.000000	4.820000e+02
pop_per_dentist	2356.0	3504.294567	2635.392607	490.000000	1819.000000	2694.500000	4220.000000	2.813000e+04
pop_per_primary_care_physician	2371.0	2587.696752	2216.147338	189.000000	1409.000000	1980.000000	2864.500000	2.339900e+04
pct_female	2546.0	0.499126	0.024247	0.285000	0.495000	0.504000	0.511000	5.720000e-01
pct_below_18_years_of_age	2546.0	0.226179	0.032725	0.088000	0.206000	0.225000	0.243750	3.590000e-01
pct_aged_65_years_and_older	2546.0	0.171583	0.041928	0.063000	0.144000	0.168000	0.194750	3.450000e-01
pct_adults_less_than_a_high_school_diploma	2546.0	0.147891	0.068077	0.016032	0.097000	0.130869	0.194410	4.659319e-01
pct_adults_with_high_school_diploma	2546.0	0.353198	0.070167	0.127127	0.308732	0.356574	0.401405	5.503490e-01
pct_adults_with_some_college	2546.0	0.300911	0.051811	0.137000	0.265734	0.301301	0.336000	4.486922e-01
pct_adults_bachelors_or_higher	2546.0	0.198000	0.086415	0.018868	0.138146	0.176677	0.232908	5.840796e-01
birth_rate_per_1k	2546.0	11.481923	2.565979	3.612183	9.915292	11.306037	12.836254	2.892287e+01
death_rate_per_1k	2546.0	10.407134	2.720135	0.000000	8.558383	10.478088	12.159568	2.739726e+01
evictions	2546.0	378.048311	1405.276610	0.000000	4.000000	29.000000	160.750000	2.925100e+04
It is very useful to study the distributions of each variable and compare pairs of variables. This can help us identify which features are more important and having more influence on our model. Through visualization we will explore each of the following questions:

1. What are the distributions of each variable?
2. How are the feature correllated with each other?
What are the distributions of each variable?
To visualize the distributions of each variable in our dataset, we have created the histograms below.

 
===================
	 	renter_occupied_households

===================
	 	pct_renter_occupied

===================
	 	median_gross_rent

===================
	 	median_household_income

===================
	 	median_property_value

===================
	 	rent_burden

===================
	 	pct_uninsured_adults

===================
	 	pct_diabetes

===================
	 	pct_excessive_drinking

===================
	 	evictions

How are the features correllated with each other?
For numeric variables, we can easily visualize across their relationships with a scatter matrix



Comparisons
We want to focus on the catergorical features and see how informative they might be in helping us to know the number of evictions and to see the correlation.

sns.factorplot(y="rucc", x="evictions", data=merged)
C:\anaconda\anaconda\lib\site-packages\seaborn\categorical.py:3666: UserWarning: The `factorplot` function has been renamed to `catplot`. The original name will be removed in a future release. Please update your code. Note that the default `kind` in `factorplot` (`'point'`) has changed `'strip'` in `catplot`.
  warnings.warn(msg)
C:\anaconda\anaconda\lib\site-packages\matplotlib\tight_layout.py:176: UserWarning: Tight layout not applied. The left and right margins cannot be made large enough to accommodate all axes decorations. 
  warnings.warn('Tight layout not applied. The left and right margins '
<seaborn.axisgrid.FacetGrid at 0x209bedfc940>

We can see here that the number of evictions tend to increase in metro counties with lots of residents on the contrary to non adjacent metro areas.

sns.factorplot(y="urban_influence", x="evictions", data=merged)
C:\anaconda\anaconda\lib\site-packages\seaborn\categorical.py:3666: UserWarning: The `factorplot` function has been renamed to `catplot`. The original name will be removed in a future release. Please update your code. Note that the default `kind` in `factorplot` (`'point'`) has changed `'strip'` in `catplot`.
  warnings.warn(msg)
C:\anaconda\anaconda\lib\site-packages\matplotlib\tight_layout.py:176: UserWarning: Tight layout not applied. The left and right margins cannot be made large enough to accommodate all axes decorations. 
  warnings.warn('Tight layout not applied. The left and right margins '
<seaborn.axisgrid.FacetGrid at 0x209b7f735c0>

We can see here that the number of evictions tend to increase in metro area with lots of residents on the contrary to non adjacent metro areas.

sns.factorplot(y="economic_typology", x="evictions", data=merged)
C:\anaconda\anaconda\lib\site-packages\seaborn\categorical.py:3666: UserWarning: The `factorplot` function has been renamed to `catplot`. The original name will be removed in a future release. Please update your code. Note that the default `kind` in `factorplot` (`'point'`) has changed `'strip'` in `catplot`.
  warnings.warn(msg)
<seaborn.axisgrid.FacetGrid at 0x209beec45c0>

We can see Non specalized has the most evictions while farm-dependent has no evictions which makes a lot of sense

sns.factorplot(y="year", x="evictions", data=merged)
C:\anaconda\anaconda\lib\site-packages\seaborn\categorical.py:3666: UserWarning: The `factorplot` function has been renamed to `catplot`. The original name will be removed in a future release. Please update your code. Note that the default `kind` in `factorplot` (`'point'`) has changed `'strip'` in `catplot`.
  warnings.warn(msg)
<seaborn.axisgrid.FacetGrid at 0x209beeea2b0>

We can see year B has slightly more evictions than year A

 
<matplotlib.axes._subplots.AxesSubplot at 0x209c2d2ef60>

 
<matplotlib.axes._subplots.AxesSubplot at 0x209c41470b8>

 
<matplotlib.axes._subplots.AxesSubplot at 0x209c403e6d8>

 

 

 

 

Correlation
The correlation is an effective way of seeing if two pairs of variables correllated in a particular period.

 
renter_occupied_households	pct_renter_occupied	median_gross_rent	median_household_income	median_property_value	rent_burden	pct_uninsured_adults	pct_diabetes	pct_excessive_drinking	evictions
renter_occupied_households	1.000000	0.404281	0.410921	0.205571	0.360398	0.168291	0.030040	-0.174596	0.023319	0.806802
pct_renter_occupied	0.404281	1.000000	0.295288	-0.050330	0.231314	0.199520	0.167806	-0.153248	-0.065100	0.368408
median_gross_rent	0.410921	0.295288	1.000000	0.735938	0.827509	0.233079	-0.216448	-0.418994	0.154647	0.301743
median_household_income	0.205571	-0.050330	0.735938	1.000000	0.680773	-0.191273	-0.485359	-0.569529	0.305521	0.131494
median_property_value	0.360398	0.231314	0.827509	0.680773	1.000000	0.164378	-0.297513	-0.468834	0.218274	0.174031
rent_burden	0.168291	0.199520	0.233079	-0.191273	0.164378	1.000000	0.021809	0.171500	-0.170600	0.155838
pct_uninsured_adults	0.030040	0.167806	-0.216448	-0.485359	-0.297513	0.021809	1.000000	0.300252	-0.389738	0.057476
pct_diabetes	-0.174596	-0.153248	-0.418994	-0.569529	-0.468834	0.171500	0.300252	1.000000	-0.420187	-0.114469
pct_excessive_drinking	0.023319	-0.065100	0.154647	0.305521	0.218274	-0.170600	-0.389738	-0.420187	1.000000	0.000693
evictions	0.806802	0.368408	0.301743	0.131494	0.174031	0.155838	0.057476	-0.114469	0.000693	1.000000
Choosing the Model
I trained 4 different models and GradientBoostingRegressor shows the best result.

Fitting completed in: 459.3602931499481 GradientBoostingRegressor(alpha=0.9, criterion='mse', init=None, learning_rate=0.05, loss='ls', max_depth=5, max_features=None, max_leaf_nodes=None, min_impurity_split=1e-07, min_samples_leaf=1, min_samples_split=3, min_weight_fraction_leaf=0.0, n_estimators=500, presort='auto', random_state=None, subsample=1.0, verbose=0, warm_start=False) MSE on train data: 13.7866 MRSE on train data: 3.71304 Score on train data: 96.8697348716 %

So we got a score of 96.86 on our test data.

Conclusion
As we can see from the analysis has demonstrated the relationships between number of evictions and several features affecting this matter. In particular, the analysis shows that regional variance play significant roles the model, which indicates that demographical distribution of customers are very important. In addition, different models absorb different sets of parameters to evaluate. While median household income, median gross rent, poverty rate and urban influence are the most important features for the model, diabetes and uninsured adults are not as important when determining thenumber of evictions.

What's next
Suppose that this report represented an exploratory pilot of the eviction problem and that the governent is sufficiently convinced that the problem is modelable. What would be our next steps?

A first step would definitely be to invest in data collection. So we would want to source or collect more data and build up a larger database. Some of the features would need changing as well. Geographic data seems really important in this model, and yet we weren’t given absolute measurements of location. Something like lat/long would be more generalizable. Finally, we would want to make some determination about our needs from the model. Determinations like how accurate do we need the model to be to be confident in our decision making? Do we care about predicting one class over the others?
