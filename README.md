# Predicting Power Outages and Their Cause
DSC80 Final Project

**Names: Ava Jeong & Charlene Hsu**

## Introduction

Power outages information and data is constantly updated as outages across the United States provide for thousands of data for various regions. This dataset on power outages provides detailed records of major power outages across the United States across several years. Information on regional, geographical data on the outages, climate factors, causes of the power outages, the durations of outages (including the start and restoration times of the outage), population affected, and economical effects of the outage are detailedly provided through this dataset.

Outages in power can have significant economic and safety effects, making this dataset highly useful for understanding patterns in outages and improving power infrastructures by understanding the factors that lead to an outage. This leads to the research question to be analyzed and answered through this project: What causes influence the duration of major power outages? And from that, using our findings, can we predict power outage durations based on these factors?

This analysis is important in allowing us to understand the major causes of power outages, allowing businesses, utility companies, policymakers, and emergency responders to better adapt to these factors as outages affect millions of people and businesses every year. Being able to understand this question and make predictions for the duration of power outages can accommodate better preparation for outages and mitigate the impact of them, which allows for improved policies, infrastructure, faster response times, and reduced economic losses.

### Dataset Overview:

The number of rows (meaning number of outages recorded) in this data is 1534 rows.
The relevant columns to assist in answering the research questions consist of ‘CLIMATE.CATEGORY’, ‘CAUSE.CATEGORY’, ‘OUTAGE.DURATION’.

- ‘CLIMATE.CATEGORY’: a categorical variable that classifies the type of climate that the power outage occurred in
- ‘CAUSE.CATEGORY’: a categorical variable that classifies the cause of the power outage
- 'DEMAND.LOSS.MW': a numerical variable that measures the scale of the impact of the outage by reporting the amount of demand loss in megawatts (MW) due to the outage
- 'CUSTOMERS.AFFECTED': a numerical variable that reports the number of customers that were affected by the outage
- ‘OUTAGE.DURATION’: a numerical variable that indicates how long the power outage lasted

Through understanding these columns and features, it allows us to identify a commonality amongst the causes and its relationship with the duration of the outages and make predictions by building a predictive model to estimate how long future outages may last.


## Data Cleaning and Exploratory Data Analysis


### Cleaned DataFrame:
|   YEAR |   MONTH | U.S._STATE   | CLIMATE.REGION     |   ANOMALY.LEVEL | CLIMATE.CATEGORY   | OUTAGE.START.DATE         | OUTAGE.START.TIME   | OUTAGE.RESTORATION.DATE    | OUTAGE.RESTORATION.TIME   | CAUSE.CATEGORY     | CAUSE.CATEGORY.DETAIL   |   HURRICANE.NAMES |   OUTAGE.DURATION |   DEMAND.LOSS.MW |   CUSTOMERS.AFFECTED |   POPULATION |   POPPCT_URBAN |   POPDEN_URBAN |   POPDEN_UC |   POPDEN_RURAL |   AREAPCT_URBAN |   AREAPCT_UC |   PCT_LAND |   PCT_WATER_TOT |   PCT_WATER_INLAND |   DEMAND_PER_CUSTOMER |   LOG_DEMAND_LOSS |   natural_cause |
|-------:|--------:|:-------------|:-------------------|----------------:|:-------------------|:--------------------------|:--------------------|:---------------------------|:--------------------------|:-------------------|:------------------------|------------------:|------------------:|-----------------:|---------------------:|-------------:|---------------:|---------------:|------------:|---------------:|----------------:|-------------:|-----------:|----------------:|-------------------:|----------------------:|------------------:|----------------:|
|   2011 |       7 | Minnesota    | East North Central |            -0.3 | normal             | Friday, July 01, 2011     | 5:00:00 PM          | Sunday, July 03, 2011      | 8:00:00 PM                | severe weather     | nan                     |               nan |              3060 |              168 |                70000 |  5.34812e+06 |          73.27 |           2279 |      1700.5 |           18.2 |            2.14 |          0.6 |    91.5927 |         8.40733 |            5.47874 |            0.0024     |           5.1299  |               1 |
|   2014 |       5 | Minnesota    | East North Central |            -0.1 | normal             | Sunday, May 11, 2014      | 6:38:00 PM          | Sunday, May 11, 2014       | 6:39:00 PM                | intentional attack | vandalism               |               nan |                 1 |              168 |                70135 |  5.45712e+06 |          73.27 |           2279 |      1700.5 |           18.2 |            2.14 |          0.6 |    91.5927 |         8.40733 |            5.47874 |            0.00239538 |           5.1299  |               0 |
|   2010 |      10 | Minnesota    | East North Central |            -1.5 | cold               | Tuesday, October 26, 2010 | 8:00:00 PM          | Thursday, October 28, 2010 | 10:00:00 PM               | severe weather     | heavy wind              |               nan |              3000 |              168 |                70000 |  5.3109e+06  |          73.27 |           2279 |      1700.5 |           18.2 |            2.14 |          0.6 |    91.5927 |         8.40733 |            5.47874 |            0.0024     |           5.1299  |               1 |
|   2012 |       6 | Minnesota    | East North Central |            -0.1 | normal             | Tuesday, June 19, 2012    | 4:30:00 AM          | Wednesday, June 20, 2012   | 11:00:00 PM               | severe weather     | thunderstorm            |               nan |              2550 |              168 |                68200 |  5.38044e+06 |          73.27 |           2279 |      1700.5 |           18.2 |            2.14 |          0.6 |    91.5927 |         8.40733 |            5.47874 |            0.00246334 |           5.1299  |               1 |
|   2015 |       7 | Minnesota    | East North Central |             1.2 | warm               | Saturday, July 18, 2015   | 2:00:00 AM          | Sunday, July 19, 2015      | 7:00:00 AM                | severe weather     | nan                     |               nan |              1740 |              250 |               250000 |  5.48959e+06 |          73.27 |           2279 |      1700.5 |           18.2 |            2.14 |          0.6 |    91.5927 |         8.40733 |            5.47874 |            0.001      |           5.52545 |               1 |


## Assessment of Missingness

A column is identified as NMAR if the chance that a value is missing depends on the actual missing value, even if it may depend on other columns. A column that is NMAR in this power outage dataset is ‘CAUSE.CATEGORY.DETAIL’, which provides further information and details on the cause of the power outage. This missingness is dependent on the value itself because it could be missing due to how specific the data collected for the cause of the outage was, or it could be because it is too complicated to pinpoint specific details for the cause category where there is not enough further information to do so. Based on this, the missingness is directly related to the missing value of the cause itself, making it NMAR.

To make the missingness MAR for ‘CAUSE.CATEGORY.DETAIL’, additional data would be needed that explains why certain causes are missing, for example, any legality issues or policies that may prevent further details to be released would need to be reported.


## Hypothesis Testing

**Null Hypothesis:** Major power outages are not affected by the cause of the outage.
**Alternative Hypothesis:** Major power outages are affected by the cause of the outage.
**Test Statistic:** Absolute difference in means

The p-value obtained was 0.0, which shows that we should reject the null hypothesis. This shows that the cause category significantly affects the outage duration, therefore we got a p-value that was significantly small, so the observed difference is unlikely due to chance.


## Framing a Prediction Problem


## Baseline Model


## Final Model


## Fairness Analysis

For our fairness analysis:
- Group X: Power outages caused by natural causes, specifically severe weather.
- Group Y: Power outages caused by any other causes other than severe weather.
- Evaluation metric: RMSE (Root Mean Squared Error)

**Null hypothesis:** Power outages that are caused by severe weather and power outages that are not caused by severe weather will have the same RMSE, which will mean that the observed differences will be due to chance.
**Alternate hypothesis:** Power outages that are caused by severe weather and power outages that are not caused by severe weather will not have the same RMSE, rather it would be higher, which will mean that the model performs more poorly with outages that are caused by severe weather.

- Test statistic: the observed difference in RMSE between outages caused by severe weather and outages not caused by severe weather
- Significance level: 0.05

### Results:

The p-value obtained was 0.406, which is much greater than the significance level of 0.05. This indicates that we fail to reject the null hypothesis, therefore meaning there is no significant evidence for unfairness in our Linear Regression model.
