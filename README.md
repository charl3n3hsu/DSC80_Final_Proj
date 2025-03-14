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

#### Prediction Type: Regression
The goal of this prediction task is to predict the duration of a power outage (OUTAGE.DURATION) based on several factors that are available at the start of the outage, including cause and climate. Since our target variable is a continuous numerical value, we define this as a regression problem rather than a classification problem. 

#### Response Variable: OUTAGE.DURATION
We chose OUTAGE.DURATION as our response variable understanding the length of outages can help the following:
- Businesses: Plan for potential financial losses
- Utility Companies: Improve infrastructure and optimize restoration efforts
- Emergency Responders: Better prepare for different situations and allocation of resources
- Policy-makers: Use data-driven insights to improve power grid reliability
Overall, we can help predict future outages and enable proactive measures to reduce economic loss and better prepare for such emergencies. 

#### Evaluation Metrics
To assess the performance of our model, we used the following metrics:
- Mean Squared Error (MSE): MSE was chosen as our primary form of evaluation metric because it helps to measure how far predicted outage durations deviate from the actual durations. It also is suitable for larger errors, allowing for outliers in the outage duration to have more weight.  
- R2 (Coefficient of Determination): R2 was chosen as our second metric because it measures how well our model performs with variability in OUTAGE.DURATION. A higher value of R2 indicates a better fit, allowing us to understand how well our model is performing with outage duration.  
MSE is prioritized, as there are significant outliers in OUTAGE.DURATION.

#### Justification of Features
The model only includes features that are known at the start of an outage. The selected features include the following:
- CAUSE.CATEGORY (Categorical): Used to identify the general cause of the outage, such as severe weather, equipment failure, etc. 
- CLIMATE.CATEGORY (Categorical): Describes the climate type in which the outage occurred, severe weathers may influence the duration
- MONTH (Numerical): Helps us to identify the seasonal trends that may affect the outages.

Some additional features that may be used, but are not known prior to the outages include the following: 
- DEMAND.LOSS.MW (Numerical): Measures the severity of the outage based on power demand loss. 
- CUSTOMERS.AFFECTED (Numerical): Larger outages may take longer to restore, more individuals being affected. 

#### Challenges
Some challenges that we faced while developing a outage duration prediction model include:  
- Handling Categorical Data
    - Most of the dataset contains categorical variables, which required us to one-hot encode.
    - We applied one-hot encoding for categorical features used such as CAUSE.CATEGORY and CLIMATE.REGION to convert them into a numerical format.
- Missing Data
    Variables including OUTAGE.DURATION had missing values in the dataset. To mitigate this, we had to perform a missingness analysis and group-wise median imputation to fill in the missing values based on the median outage duration for each cause category.
- Skewed Data
    - Our target variable also has extreme outliers, meaning that we may need to apply log transformation to deal with the outliers.

## Baseline Model

#### Chosen Model: Linear Regression with a Pipeline
For our baseline model, we chose to implement a Linear Regression model using an sklearn Pipeline, to ensure that all preprocessing steps such as encoding categorical variables were integrated within our training steps. 

##### Features Used
Our model uses the following two categorical features to predict the duration of outages:
- CAUSE.CATEGORY (Nomial, Categorical)
    - Represents the general cause of the power outage, such as severe weather, equipment failure, intentional attack, etc. 
    - Encoding Method: One-hot encoding, since there is no order among these categories. 
- CLIMATE.REGION (Nominal, Categorical)
    - Represents the climate region where the outage occurred, such as the Northeast, West, South, etc. 	
    - Encoding Method: One-hot encoding, since there is no order among these categories. 


#### Encoding and Model Training
- One-hot encoding was applied to the categorical variables, as mentioned above using a ColumnTransformer. 
- We split the dataset into training (80%) and testing (20%) sets to evaluate model generalization.
- The final pipeline consists of
    - Preprocessing step: One-hot encoding of categorical features
    - Regressoin: Linear Regression to predict OUTAGE.DURATION 

#### Baseline Model Performance and Assessment
After training and evaluating our baseline model on the test set, we obtained the following results:
- Mean Squared Error (MSE): 26,061,252.55965856
- $R^2$ Score: 0.007262599857186136

The baseline model’s low $R^2$ score of 0.0077 shows that it does not do a good job of explaining the variance in outage durations. This suggests that additional features may be needed to improve our model’s performance. Some limitations of our baseline model include limited feature selection and the complex relationship between our chosen features and outage duration. The baseline model only considers CAUSE.CATEGORY and CLIMATE.REGION, which do not account for other potential predictive features such as DEMAND.LOSS.MW and CUSTOMERS.AFFECTED. The performance of our model suggests that outage duration is likely influenced by multiple interacting factors, which this baseline model currently fails to capture. In addition to the lack of necessary features, power outages and their durations may not follow a simple linear relationship.

## Final Model

#### Improvements from Baseline Model
To enhance our baseline model, we incorporated feature engineering, explored non-linear relationships, and performed hyperparameter tuning to optimize the model’s performance. 

Notable Improvements include the following:
- Addition of New Features
    - DEMAND.LOSS.MW (Megawatts lost due to outage): A key indicator of outage severity. 
    - CUSTOMERS.AFFECTED (Number of customers affected by the outage): Higher value could indicate longer restoration times, as more people are affected.
    - DEMAND_PER_CUSTOMER (Ratio of demand loss per customer): Captures the outage impact per customer
    - LOG_DEMAND_LOSS (Log-transformed demand loss): Put in place to normalize skewed data for better regression analysis
    - MONTH (Month in which the outage occurred): Captures the seasonal patterns affecting the outage duration. 
- Handling Missing Values
    - We used median imputation to handle missing values in DEMAND.LOSS.MW and CUSTOMERS.AFFECTED to ensure consistency within our dataset.
    - We replaced infinite values with NaN and re-imputed them to avoid computational errors from occurring. 
- Modeling Approach
    - We applied Polynomial Regression to capture non-linear relationships in the data, rather than using a simple Linear Regression model. 
    - We used PolynomialFeatures() within an sklearn Pipeline to generate the polynomial terms.
- Hyperparameter Tuning
    - We applied GridSearchCV to find the best polynomial degree (poly_degree), testing values of 1, 2, and 3. 
    - The best-performing model had a polynomial degree of 1, which suggests that a linear relationship best fits our dataset. 

#### Final Model Performance Assessment
After training and evaluating our final model on the test set, we obtained the following results:
- Mean Squared Error (MSE): 24966319.61238235
- $R^2$ Score: 0.071

Although the $R^2$ score is still relatively low, we can see a noticeable improvement compared to the results from our baseline model (MSE: 26,061,252.56, R²: 0.0077). The decrease in our MSE value indicates that the model’s predictions are closer to the actual outage durations than before, meaning the model has better accuracy. The increase in our $R^2$ score suggests that the model captures more variance in outage duration, although there is still a significant amount of unexplained variance, indicating that additional features or a different modeling approach could further improve our performance. 


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
