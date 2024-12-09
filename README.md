# Whats the Cause of your Power Outage?
by: Kaii Bijlani and Ketan Mittal

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
## Dataset Overview  

The dataset contains **1,534 observations** and includes relevant columns related to power outages, their causes, durations, and economic impacts.  


| **Column Name**              | **Description**                                               |
|------------------------------|---------------------------------------------------------------|
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