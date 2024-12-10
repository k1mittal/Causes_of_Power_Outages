DSC 80 Project: Investigating power outages and predicting their causes

## **Introduction**
### Introduction to the Dataset

Our project utilizes a dataset containing information on major power outages in the continental United States from January 2000 to July 2016. Power outages can disrupt daily life, impact economies, and even endanger lives, making it crucial to understand their causes and implications. By examining this dataset, we aim to explore trends and relationships that can help companies better prepare for and mitigate the effects of power outages.

### Research Question

Our central research question is:
How does the cause of power outages relate to other factors, such as the number of people affected? Can we predict the cause of power outages based on related data?

This question is important because understanding the relationship between causes and impacts can help utility companies prioritize resources during outages. Additionally, predicting causes can enhance response strategies and improve resilience to such disruptions.

### Why This Matters to Readers

Readers should care about this dataset and research because power outages are a common yet impactful issue that affects millions of people each year. By uncovering patterns and predicting outage causes, our analysis can contribute to reducing the duration and impact of future outages. Stakeholders such as policymakers, utility companies, and emergency response teams can use these insights to allocate resources more effectively and improve infrastructure.

### Dataset Overview

The dataset contains **1,534 observations** and includes relevant columns related to power outages, their causes, durations, and economic impacts.  

| **Column Name**              | **Description**                                               |
|:------------------------------|:---------------------------------------------------------------|
| OBS                      | Unique observation identifier for each outage event.          |
| YEAR                     | Year when the outage occurred.                                |
| MONTH                    | Month when the outage occurred.                               |
| U.S._STATE               | U.S. state where the outage happened.                        |
| NERC.REGION              | North American Electric Reliability Corporation (NERC) region associated with the outage location. |
| CLIMATE.REGION           | Climate classification region where the outage occurred.      |
| ANOMALY.LEVEL            | Level of climatic anomaly during the outage event.            |
| OUTAGE.START.DATE        | Date when the outage started.                                 |
| OUTAGE.START.TIME        | Time when the outage began.                                   |
| OUTAGE.RESTORATION.DATE  | Date when power was restored.                                |
| OUTAGE.RESTORATION.TIME  | Time when power restoration was completed.                   |
| CAUSE.CATEGORY           | General category of the outage cause (e.g., weather-related, equipment failure). |
| CLIMATE.CATEGORY         | Climate-related classification relevant to the outage event. |
| CAUSE.CATEGORY.DETAIL    | Detailed description of the cause of the outage.             |
| OUTAGE.DURATION          | Total duration of the outage in hours.                       |
| DEMAND.LOSS.MW           | Amount of power demand lost during the outage (in megawatts).|
| CUSTOMERS.AFFECTED       | Number of customers affected by the outage.                  |
| TOTAL.PRICE              | Total price of electricity during the outage period.         |
| TOTAL.SALES              | Total electricity sales during the outage period.            |
| TOTAL.CUSTOMERS          | Total number of electricity customers in the affected area.  |
| TOTAL.REALGSP            | Total real Gross State Product (GSP) of the affected region. |

## Data Cleaning and Exploratory Data Analysis
### Data Cleaning
The following data cleaning steps were taken to prepare the dataset for analysis, ensuring accuracy and consistency based on the data-generating process:  

1. **Handling Missing Values**:  
   - Dropped rows with missing values in essential columns related to outage timing: `OUTAGE.START.DATE`, `OUTAGE.START.TIME`, `OUTAGE.RESTORATION.DATE`, and `OUTAGE.RESTORATION.TIME`.  
   - This step removed incomplete records where outage timing data was missing, ensuring accurate calculations for outage durations and time-series analyses.  

2. **Combining Date and Time Columns**:  
   - Created a new `OUTAGE.START` column by merging `OUTAGE.START.DATE` and `OUTAGE.START.TIME` into a single datetime field.  
   - Created a new `OUTAGE.END` column by merging `OUTAGE.RESTORATION.DATE` and `OUTAGE.RESTORATION.TIME`.  
   - Dropped the original date and time columns to reduce redundancy.  
   - This process enabled precise calculations of outage durations and facilitated time-series analysis.  

3. **Seasonal Binning**:  
   - Created a new column `SEASONAL.BINS` by binning the `MONTH` column into four seasons:  
     - Winter (January, February, December)  
     - Spring (March, April, May)  
     - Summer (June, July, August)  
     - Fall (September, October, November)  
   - This transformation supported seasonal trend analysis.  

4. **Correcting Zero Values**:  
   - Replaced zeros in `CUSTOMERS.AFFECTED` and `OUTAGE.DURATION` with `NaN`.  
   - This correction addressed data inaccuracies caused by erroneous zero entries, ensuring meaningful statistical summaries and analysis.  

---

|   OBS |   YEAR |   MONTH | U.S._STATE   | NERC.REGION   | CLIMATE.REGION     |   ANOMALY.LEVEL | CAUSE.CATEGORY     | CLIMATE.CATEGORY   | CAUSE.CATEGORY.DETAIL   |   OUTAGE.DURATION |   DEMAND.LOSS.MW |   CUSTOMERS.AFFECTED |   TOTAL.PRICE |   TOTAL.SALES |   TOTAL.CUSTOMERS |   TOTAL.REALGSP | OUTAGE.START        | OUTAGE.END          | SEASONAL.BINS   |
|:------|:-------|:--------|:-------------|:--------------|:-------------------|:----------------|:-------------------|:-------------------|:------------------------|:------------------|:-----------------|:---------------------|:--------------|:--------------|:------------------|:----------------|:--------------------|:--------------------|:----------------|
|     1 |   2011 |       7 | Minnesota    | MRO           | East North Central |            -0.3 | severe weather     | normal             | nan                     |              3060 |              nan |                70000 |          9.28 |       6562520 |       2.5957e+06  |          274182 | 2011-07-01 17:00:00 | 2011-07-03 20:00:00 | Summer          |
|     2 |   2014 |       5 | Minnesota    | MRO           | East North Central |            -0.1 | intentional attack | normal             | vandalism               |                 1 |              nan |                  nan |          9.28 |       5284231 |       2.64074e+06 |          291955 | 2014-05-11 18:38:00 | 2014-05-11 18:39:00 | Summer          |
|     3 |   2010 |      10 | Minnesota    | MRO           | East North Central |            -1.5 | severe weather     | cold               | heavy wind              |              3000 |              nan |                70000 |          8.15 |       5222116 |       2.5869e+06  |          267895 | 2010-10-26 20:00:00 | 2010-10-28 22:00:00 | Fall            |
|     4 |   2012 |       6 | Minnesota    | MRO           | East North Central |            -0.1 | severe weather     | normal             | thunderstorm            |              2550 |              nan |                68200 |          9.19 |       5787064 |       2.60681e+06 |          277627 | 2012-06-19 04:30:00 | 2012-06-20 23:00:00 | Summer          |
|     5 |   2015 |       7 | Minnesota    | MRO           | East North Central |             1.2 | severe weather     | warm               | nan                     |              1740 |              250 |               250000 |         10.43 |       5970339 |       2.67353e+06 |          292023 | 2015-07-18 02:00:00 | 2015-07-19 07:00:00 | Summer          |

### Univariate Analysis

- Power Outages by U.S. State (Folium Map)  

The map below shows the frequency of power outages across different U.S. states. States such as Texas and California experience higher outage counts, likely due to larger populations, more extensive power grids, and increased vulnerability to extreme weather events like storms and wildfires. This visualization highlights regional disparities in power reliability across the country.  

<!-- Embed the Folium map HTML file -->
<iframe src="assets/state_frequency.html" width="100%" height="500" frameborder="0"></iframe>

---

- Power Outages by Cause (Histogram)  

The histogram below shows the frequency of power outages by cause category. Weather-related causes are the most common, underscoring the significant impact of natural events like storms, hurricanes, and wildfires on power reliability. Equipment failures are another major cause, reflecting aging infrastructure in certain regions. This distribution emphasizes the need for targeted improvements in infrastructure and disaster preparedness.  

<!-- Embed the Histogram Plotly HTML file -->
<iframe src="assets/cause_frequency.html" width="100%" height="500" frameborder="0"></iframe>


### Bivariate Analysis
 
- Anomaly Level by Season (Violin Plot)  

The violin plot below illustrates the distribution of `Anomaly Level` across different seasons. Fall and winter show a wider range of anomaly levels compared to summer and spring. This pattern indicates that extreme weather events such as winter storms and unpredictable fall weather contribute to greater variability in power outages during these seasons.  

<!-- Embed the Violin Plot HTML file -->
<iframe src="assets/violin.html" width="100%" height="500" frameborder="0"></iframe>

---

- Outage Duration by Climate Region (Scatter Plot)  

The scatter plot above shows the relationship between `Climate Region` and `Outage Duration`. Outage durations vary significantly across regions, with some regions experiencing notably longer outages, such as the Northeast and West. This pattern may be influenced by extreme weather events or infrastructure challenges in these areas, highlighting the impact of regional environmental and structural factors on power outage severity. 

<!-- Embed the Scatter Plot HTML file -->
<iframe src="assets/scatter.html" width="100%" height="500" frameborder="0"></iframe>

### Interesting Aggregates
The table below summarizes the `average total price` (in millions) of power outages grouped by `Cause Category` and `Climate Region`. It provides insights into how outage costs vary depending on the underlying cause and the regional climate. For instance, `equipment failures` and `severe weather` consistently result in higher costs across most regions, particularly in the `Northeast` and `West`, which may be due to their population density and infrastructure challenges. This information can help prioritize investments in preventive measures tailored to specific causes and regions.  

|   Central |   East North Central |   Northeast |   Northwest |   South |   Southeast |   Southwest |    West |   West North Central |
|:----------|:---------------------|:------------|:------------|:--------|:------------|:------------|:--------|:---------------------|
|   7.652   |              7.92333 |     12.354  |     6.905   | 8.24111 |    10.15    |     8.068   | 12.7424 |                6.21  |
|   7.445   |             10.5075  |     16.0343 |     7.29    | 9.17    |   nan       |     8.65    | 13.816  |              nan     |
|   8.95206 |              9.271   |     12.8254 |     7.24434 | 8.64071 |     9.23375 |     8.57164 | 12.9065 |                7.42  |
|   6.90667 |             10.56    |     12.82   |     7.16    | 7.645   |   nan       |     9.61    | 13.7418 |                7.838 |
|   9.49    |             10.605   |     13.0925 |     5.715   | 8.4081  |     8.338   |     7.73    | 12.8944 |                8.015 |
|   8.27188 |              9.33592 |     12.4494 |     6.8304  | 8.62728 |     8.36417 |     8.126   | 12.7878 |                6.365 |
|   8.402   |              8.24    |     13.71   |     6.325   | 8.65852 |     9.1075  |     8.67778 | 12.3703 |              nan     |

## Assessment of Missingness
### NMAR Analysis
The column `outage.start` in a power outage dataframe could be **NMAR** (Not Missing At Random) as the date can be missing on itself. The reported dates may be missing due to itself, therefore making it **NMAR**. Understanding the severity of the outages, such as those lasting longer or requiring more restoration time, might have missing start times due to delays in data recording or prioritization of other tasks during the outage. This could indicate that the missingness is not random, but instead related to the characteristics of the outage itself. By analyzing the severity of outages and how it correlates with missing start times, we could better understand whether the missing data is systematically related to the observed severity, potentially making it **MAR** (Missing At Random). 

### Missingness Dependency

- Model 1: `CAUSE.CATEGORY.DETAIL` vs `U.S._STATE`

The missingness analysis for the `CAUSE.CATEGORY.DETAIL` with respect to `U.S._STATE` resulted in a p-value of `0.0`, indicating that the missingness pattern for this variable is **Missing at Random (MAR)**. This suggests that the missing cause category details can be related to the state, which is important for guiding the handling of missing values in subsequent analyses.

<!-- Embed the Scatter Plot HTML file -->
<iframe src="assets/MAR1.html" width="100%" height="500" frameborder="0"></iframe>
---

- Model 2: `OUTAGE.DURATION` vs `MONTH`

For the `OUTAGE.DURATION` with respect to `MONTH`, the analysis produced a p-value of `0.606`, suggesting that the missingness of duration is not related to month. This result implies that the missingness is likely related to other unobserved factors, informing decisions about the assumptions and strategies for handling the missing data.

<!-- Embed the Scatter Plot HTML file -->
<iframe src="assets/MAR2.html" width="100%" height="500" frameborder="0"></iframe>

## Hypothesis Testing

- Test #1

Null Hypothesis ($H_0$) - The proportion of each cause category is uniformly distributed across each season, for each cause category.

Alternative Hypothesis ($H_a$) - The proportion of each cause category is not uniformly distributed across each season, for each cause category.

To evaluate the hypothesis, we used the Total Variation Distance (TVD) as the test statistic. TVD measures the difference between the observed and expected distributions of cause categories across seasons. The test compares how much the observed distribution deviates from the expected distribution under the assumption that the cause categories are uniformly distributed across seasons.

We used a significance level of 0.05 for this hypothesis test. A significance level of 0.05 is commonly chosen in hypothesis testing, as it provides a balance between type I and type II errors, meaning we have a 5% chance of incorrectly rejecting the null hypothesis.

#### Results

1. **Observed TVD**: 
   The observed Total Variation Distance (TVD) was calculated from the actual data distribution.

2. **Simulated TVD**: 
   We performed 1,000 simulations by permuting the season labels within the dataset to generate a distribution of TVD under the null hypothesis (uniform distribution of cause categories across seasons).

3. **P-value**: 
   The p-value is calculated as the proportion of simulated TVD values that are greater than the observed TVD.

The p-value calculated is approximately 0.0.

Since the p-value (0.0) is less than our significance level of 0.05, we can reject the null hypothesis. This suggests that there is a significant evidence to conclude that the proportion of each cause category is not uniformly distributed across seasons. In other words, the observed differences in the distributions of cause categories across seasons could not have reasonably have occurred by chance.


The histogram below shows the distribution of the Total Variation Distance (TVD) from the 1,000 simulations. The red line represents the observed TVD value.

<iframe src="assets/hypothesis.html" width="100%" height="500" frameborder="0"></iframe>

- Test #2

Null Hypothesis ($H_0$) - The distributions of mean affected customers for each state are the same for observations from 2005 and 2006.

Alternative Hypothesis ($H_a$) - The distributions of mean affected customers for each state are different for observations from 2005 and 2006.

To evaluate the hypothesis, we used the Total Variation Distance (TVD) as the test statistic. TVD measures the difference between the observed distributions of mean affected customers in 2005 and 2006 across states. The test compares how much the observed distribution of mean affected customers for 2006 deviates from the expected distribution for 2005, assuming that the distributions should be the same under the null hypothesis.

The p-value calculated is approximately 0.0.

Since the p-value (0.0) is much smaller than our significance level of 0.05, we reject the null hypothesis. This provides strong evidence to conclude that the distributions of mean affected customers for each state are significantly different between the observations in 2005 and 2006. The observed differences in the customer distributions across these two periods are highly unlikely to have occurred by chance.

<iframe src="assets/hypothesis2.html" width="100%" height="500" frameborder="0"></iframe>>

## Framing a Prediction Problem

This is a Multiclass Classification problem 

Response Variable:  
`CAUSE.CATEGORY` - This variable represents the general cause of power outages. We chose this variable because understanding the cause of outages can help improve outage management, preparedness, and mitigation efforts.  

Features Used:  
We will only use features that can be found after a power outage, meaning we will not use features like `CAUSE.CATEGORY.DETAIL`. We will also use only relevant features, ensuring that the model is trained and does not have confouding variables.  

Model Choice:  
**Random Forest Multiclass Classifier**  
We chose this model because of its ability to handle categorical variables, manage feature importance, and deal with imbalanced data effectively.  

Evaluation Metrics:  

1. **R² Score**:  
   - **Why**: Measures the proportion of variance explained by the model, providing insight into the overall performance of the model.  
   - **Justification**: Useful for understanding how well the features explain the causes of outages, though less common for classification tasks.  

2. **F1-Score**:  
   - **Why**: Balances precision and recall, making it suitable for evaluating multiclass classification where class imbalances may exist.  
   - **Justification**: Chosen over accuracy because of potential imbalanced class distributions, ensuring that both false positives and false negatives are considered.  

By using these metrics, we aim to comprehensively evaluate the model's predictive performance and robustness.  

## Baseline Model

## Final Model

## Fairness Analysis
