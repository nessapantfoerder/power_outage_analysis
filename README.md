# Power Outage Analysis
UCSD DSC 80 Project 3

by Nessa Pantfoerder

---

## Introduction

This dataset outlines major power outages in the continental U.S. from January 2000 to July 2016 providing information on population, region, land area, consumption, outage duration and causes, as well as regional climate information.

*Question:*

- Does the cause of major outages affect the duration of the outage?

*Rows:*

There are 1534 rows in this dataset.

*Relevant Columns and Descriptions:*

- YEAR	
    - Indicates the year when the outage event occurred
- MONTH
    - Indicates the month when the outage event occurred
- NERC.REGION
    - The North American Electric Reliability Corporation (NERC) regions involved in the outage event
- CLIMATE.REGION
    - U.S. Climate regions as specified by National Centers for Environmental Information (nine climatically consistent regions in continental U.S.A.)
- CLIMATE.CATEGORY
    - This represents the climate episodes corresponding to the years. The categories—“Warm”, “Cold” or “Normal” episodes of the climate are based on a threshold of ± 0.5 °C for the Oceanic Niño Index (ONI)
- OUTAGE.START.DATE
    - This variable indicates the day of the year when the outage event started (as reported by the corresponding Utility in the region)
- OUTAGE.START.TIME
    - This variable indicates the time of the day when the outage event started (as reported by the corresponding Utility in the region)
- OUTAGE.RESTORATION.DATE
    - This variable indicates the day of the year when power was restored to all the customers (as reported by the corresponding Utility in the region)
- OUTAGE.RESTORATION.TIME
    - This variable indicates the time of the day when power was restored to all the customers (as reported by the corresponding Utility in the region)
- OUTAGE.DURATION	
    - Duration of outage events (in minutes)
- CAUSE.CATEGORY
    - Categories of all the events causing the major power outages
- CAUSE.CATEGORY.DETAIL
    - Detailed description of the event categories causing the major power outages
- HURRICANE.NAMES
    - If the outage is due to a hurricane, then the hurricane name is given by this variable


---

## Cleaning and EDA

### Data Cleaning

I combined columns 'OUTAGE.START.DATE' and 'OUTAGE.START.TIME' into one column 'OUTAGE.START' of type pd.Timestamp

I did the same combining 'OUTAGE.RESTORATION.DATE' and 'OUTAGE.RESTORATION.TIME' into 'OUTAGE.RESTORATION'

I then replaced all missing 'NA' values with np.NaN

|   OBS |   YEAR |   MONTH | U.S._STATE   | POSTAL.CODE   | NERC.REGION   | CLIMATE.REGION     |   ANOMALY.LEVEL | CLIMATE.CATEGORY   | CAUSE.CATEGORY     | CAUSE.CATEGORY.DETAIL   |   HURRICANE.NAMES |   OUTAGE.DURATION |   DEMAND.LOSS.MW |   CUSTOMERS.AFFECTED |   RES.PRICE |   COM.PRICE |   IND.PRICE |   TOTAL.PRICE |   RES.SALES |   COM.SALES |   IND.SALES |   TOTAL.SALES |   RES.PERCEN |   COM.PERCEN |   IND.PERCEN |   RES.CUSTOMERS |   COM.CUSTOMERS |   IND.CUSTOMERS |   TOTAL.CUSTOMERS |   RES.CUST.PCT |   COM.CUST.PCT |   IND.CUST.PCT |   PC.REALGSP.STATE |   PC.REALGSP.USA |   PC.REALGSP.REL |   PC.REALGSP.CHANGE |   UTIL.REALGSP |   TOTAL.REALGSP |   UTIL.CONTRI |   PI.UTIL.OFUSA |   POPULATION |   POPPCT_URBAN |   POPPCT_UC |   POPDEN_URBAN |   POPDEN_UC |   POPDEN_RURAL |   AREAPCT_URBAN |   AREAPCT_UC |   PCT_LAND |   PCT_WATER_TOT |   PCT_WATER_INLAND | OUTAGE.START        | OUTAGE.RESTORATION   |
|------:|-------:|--------:|:-------------|:--------------|:--------------|:-------------------|----------------:|:-------------------|:-------------------|:------------------------|------------------:|------------------:|-----------------:|---------------------:|------------:|------------:|------------:|--------------:|------------:|------------:|------------:|--------------:|-------------:|-------------:|-------------:|----------------:|----------------:|----------------:|------------------:|---------------:|---------------:|---------------:|-------------------:|-----------------:|-----------------:|--------------------:|---------------:|----------------:|--------------:|----------------:|-------------:|---------------:|------------:|---------------:|------------:|---------------:|----------------:|-------------:|-----------:|----------------:|-------------------:|:--------------------|:---------------------|
|     1 |   2011 |       7 | Minnesota    | MN            | MRO           | East North Central |            -0.3 | normal             | severe weather     | nan                     |               nan |              3060 |              nan |                70000 |       11.6  |        9.18 |        6.81 |          9.28 | 2.33292e+06 | 2.11477e+06 | 2.11329e+06 |   6.56252e+06 |      35.5491 |      32.225  |      32.2024 |         2308736 |          276286 |           10673 |           2595696 |        88.9448 |        10.644  |         0.4112 |              51268 |            47586 |          1.07738 |                 1.6 |           4802 |          274182 |       1.75139 |             2.2 |      5348119 |          73.27 |       15.28 |           2279 |      1700.5 |           18.2 |            2.14 |          0.6 |    91.5927 |         8.40733 |            5.47874 | 2011-07-01 17:00:00 | 2011-07-03 20:00:00  |
|     2 |   2014 |       5 | Minnesota    | MN            | MRO           | East North Central |            -0.1 | normal             | intentional attack | vandalism               |               nan |                 1 |              nan |                  nan |       12.12 |        9.71 |        6.49 |          9.28 | 1.58699e+06 | 1.80776e+06 | 1.88793e+06 |   5.28423e+06 |      30.0325 |      34.2104 |      35.7276 |         2345860 |          284978 |            9898 |           2640737 |        88.8335 |        10.7916 |         0.3748 |              53499 |            49091 |          1.08979 |                 1.9 |           5226 |          291955 |       1.79    |             2.2 |      5457125 |          73.27 |       15.28 |           2279 |      1700.5 |           18.2 |            2.14 |          0.6 |    91.5927 |         8.40733 |            5.47874 | 2014-05-11 18:38:00 | 2014-05-11 18:39:00  |
|     3 |   2010 |      10 | Minnesota    | MN            | MRO           | East North Central |            -1.5 | cold               | severe weather     | heavy wind              |               nan |              3000 |              nan |                70000 |       10.87 |        8.19 |        6.07 |          8.15 | 1.46729e+06 | 1.80168e+06 | 1.9513e+06  |   5.22212e+06 |      28.0977 |      34.501  |      37.366  |         2300291 |          276463 |           10150 |           2586905 |        88.9206 |        10.687  |         0.3924 |              50447 |            47287 |          1.06683 |                 2.7 |           4571 |          267895 |       1.70627 |             2.1 |      5310903 |          73.27 |       15.28 |           2279 |      1700.5 |           18.2 |            2.14 |          0.6 |    91.5927 |         8.40733 |            5.47874 | 2010-10-26 20:00:00 | 2010-10-28 22:00:00  |
|     4 |   2012 |       6 | Minnesota    | MN            | MRO           | East North Central |            -0.1 | normal             | severe weather     | thunderstorm            |               nan |              2550 |              nan |                68200 |       11.79 |        9.25 |        6.71 |          9.19 | 1.85152e+06 | 1.94117e+06 | 1.99303e+06 |   5.78706e+06 |      31.9941 |      33.5433 |      34.4393 |         2317336 |          278466 |           11010 |           2606813 |        88.8954 |        10.6822 |         0.4224 |              51598 |            48156 |          1.07148 |                 0.6 |           5364 |          277627 |       1.93209 |             2.2 |      5380443 |          73.27 |       15.28 |           2279 |      1700.5 |           18.2 |            2.14 |          0.6 |    91.5927 |         8.40733 |            5.47874 | 2012-06-19 04:30:00 | 2012-06-20 23:00:00  |
|     5 |   2015 |       7 | Minnesota    | MN            | MRO           | East North Central |             1.2 | warm               | severe weather     | nan                     |               nan |              1740 |              250 |               250000 |       13.07 |       10.16 |        7.74 |         10.43 | 2.02888e+06 | 2.16161e+06 | 1.77794e+06 |   5.97034e+06 |      33.9826 |      36.2059 |      29.7795 |         2374674 |          289044 |            9812 |           2673531 |        88.8216 |        10.8113 |         0.367  |              54431 |            49844 |          1.09203 |                 1.7 |           4873 |          292023 |       1.6687  |             2.2 |      5489594 |          73.27 |       15.28 |           2279 |      1700.5 |           18.2 |            2.14 |          0.6 |    91.5927 |         8.40733 |            5.47874 | 2015-07-18 02:00:00 | 2015-07-19 07:00:00  |

### Univariate Analysis

Customers affected by Outages shows that it is more likely that fewer customers will be affected. Meaning that an outage that affects the  maximum amount of customers is much rarer than outages that affect the minimum amount of cutsomers.

<iframe src="assets/univariate.html" width=800 height=600 frameBorder=0></iframe>

### Bivariate Analysis

Customers Affected by Outage Duration in Minutes shows that the majority of outages are short in duration in minimal in customers affected. Outliers that are greater in customers affected tend to also be greater in duration with a few short outages.

<iframe src="assets/bivariate.html" width=800 height=600 frameBorder=0></iframe>

### Interesting Aggregates

Pivoting on Cause Category and Month shows us that severe weather is the leading cause of outages and that the month with the most outages is June with the leading cause that month being severe weather.

| CAUSE.CATEGORY                |   1.0 |   2.0 |   3.0 |   4.0 |   5.0 |   6.0 |   7.0 |   8.0 |   9.0 |   10.0 |   11.0 |   12.0 |
|:------------------------------|------:|------:|------:|------:|------:|------:|------:|------:|------:|-------:|-------:|-------:|
| equipment failure             |     3 |     4 |     4 |     7 |     6 |     7 |    12 |     4 |     4 |    nan |      2 |      4 |
| fuel supply emergency         |     4 |     9 |     5 |     3 |     2 |     7 |     6 |     5 |     3 |    nan |      2 |      4 |
| intentional attack            |    50 |    40 |    42 |    43 |    46 |    34 |    34 |    26 |    21 |     34 |     24 |     24 |
| islanding                     |   nan |     6 |     3 |     2 |     5 |    10 |     4 |     4 |     3 |      3 |      3 |      3 |
| public appeal                 |     4 |     5 |     2 |   nan |     5 |    16 |    14 |    18 |     1 |      2 |    nan |      2 |
| severe weather                |    67 |    61 |    30 |    44 |    51 |   102 |    98 |    83 |    58 |     62 |     38 |     65 |
| system operability disruption |     8 |    11 |    14 |    12 |    12 |    19 |    13 |    13 |     4 |      8 |      3 |      9 |

---

## Assessment of Missingness

### NMAR Analysis

RES.PRICE, COM.PRICE, IND.PRICE, and TOTAL.PRICE could be NMAR because sectors that charge unreasonable prices for electricity will not want to report. A coloumn we could add that could make it MAR is utiltiy to income proportion so we can see where people are paying higher for utitlites while making lower income.

### Missingness Dependency

*CLIMATE.CATEGORY and CAUSE.CATEGORY*
- The null states that the distribution of 'CAUSE.CATEGORY' when 'CLIMATE.CATEGORY' is missing is the same as the distribution of 'CAUSE.CATEGORY' when 'CLIMATE.CATEGORY' is not missing.
- The alternative hypothesis states that the distribution of 'CAUSE.CATEGORY' when 'CLIMATE.CATEGORY' is missing is a different distribution than 'CAUSE.CATEGORY' when 'CLIMATE.CATEGORY' is not missing.
- Significance level of 0.05.
- P-value is 0.336.
- We fail to reject the null.
- We conclude that the missingness in the 'CAUSE.CATEGORY' column is not dependent on 'CLIMATE.CATEGORY'.
- Thus MCAR.

<iframe src="assets/missingness-MCAR.html" width=800 height=600 frameBorder=0></iframe>

*CLIMATE.CATEGORY and NERC.REGION*
- The null states that the distribution of 'NERC.REGION' when 'CLIMATE.CATEGORY' is missing is the same as the distribution of 'NERC.REGION' when 'CLIMATE.CATEGORY' is not missing.
- The alternative hypothesis states that the distribution of 'NERC.REGION' when 'CLIMATE.CATEGORY' is missing is a different distribution than 'NERC.REGION' when 'CLIMATE.CATEGORY' is not missing.
- Significance level of 0.05.
- P-value is 0.034.
- We reject the null.
- We conclude that the missingness in the 'CLIMATE.CATEGORY' column is not dependent on 'NERC.REGION'.
- Thus MAR

<iframe src="assets/missingness-MAR.html" width=800 height=600 frameBorder=0></iframe>

---

## Hypothesis Testing

**Null Hypothesis**
- In the population durations of outages caused by 'severe weather' and those with any other cause have the same distribution, and the observed differences in our samples are due to random chance.
- 'Severe Weather' vs all other cause categories have no relationship to duration of the outage.
- In other words 'severe weather' and all other cause category labels may well have been assigned at random.
- Simple terms: outage durations come from the same distribution.

**Alternative Hypothesis**
- In the population, outages caused by 'severe weather' have longer outage durations than others, on average. 
- The observed difference in our samples cannot be explained by random chance alone. 
- Outages caused by 'severe weather' and those that aren't come from different population distributions. 
- That is, they come from different data generating processes. 
- Simple terms: outage durations come from different distributions.

**Test Statistic**
- Our test statistic will be:
    - *mean outage duration of outages caused by severe weather* − *mean outage duration of outages not caused by severe weather*

**Significance Level**
- Our significance level will be 0.05.

**P-Value**
- The p-value is 0.0.

**Conclusion**
- Under the null hypothesis, we rarely see differences as large as 2537 duration. 
- Therefore, we reject the null hypothesis that the two groups come from the same distribution. 
- Thus the observed differences in our samples are not due to random chance. 
- And we can conclude that outages caused by 'severe weather' vs outages not caused by severe weather have some relationship to the duration of the outages.

<iframe src="assets/permutation-test.html" width=800 height=600 frameBorder=0></iframe>

---