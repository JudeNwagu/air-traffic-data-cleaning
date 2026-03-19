# Air Traffic Data Cleaning Project







\## Project Summary



Airports operate in a highly seasonal and capacity constrained environment. Decisions around scheduling, fleet allocation, and route planning depend on reliable historical data. However, raw operational datasets are rarely analysis ready.



In this project, I worked with an aircraft landing dataset from San Francisco International Airport. The dataset captures monthly landing counts and total landed weight across airlines, regions, and aircraft types. Because the data is self reported and aggregated, it contains typical real world issues such as missing values, inconsistent formats, and complex relationships between fields.



The objective was to transform this raw dataset into a clean, structured, and trustworthy dataset that can support business analysis.



\---



\## Business Context



A clean version of this dataset can be used to answer questions such as:



\* Which airlines dominate airport traffic over time

\* How landing activity changes across seasons

\* What aircraft types contribute most to total landed weight

\* How operational load varies across regions



These insights can inform airline partnerships, infrastructure planning, and capacity management decisions.



\---



\## Problem



The raw dataset presented several challenges:



\* Missing values in key categorical fields

\* Inconsistent column naming conventions

\* Incorrect data types for time based analysis

\* Potential duplicate records

\* Presence of extreme values that require validation

\* Non one to one relationships across some attributes



Without addressing these issues, any analysis built on top of the data would be unreliable.



\---



\## Approach



I followed a structured data cleaning workflow used in real analytical environments.



\### 1. Data Loading



```python

import pandas as pd



df = pd.read\_csv("air\_traffic.csv")

```



\### 2. Data Inspection



```python

df.head()

df.info()

df.shape

```



Goal: Understand structure, data types, and initial data quality.



\---



\### 3. Missing Value Assessment



```python

df.isnull().sum()

```



Goal: Identify columns with missing data and determine handling strategy.



\---



\### 4. Column Standardization



```python

df.columns = df.columns.str.lower().str.replace(" ", "\_")

```



Goal: Ensure consistency and improve usability.



\---



\### 5. Data Type Correction



```python

df\["date"] = pd.to\_datetime(df\["date"])

```



Goal: Enable time based analysis and avoid downstream errors.



\---



\### 6. Handling Missing Values



```python

df.loc\[:, "operating\_airline\_iata\_code"] = df\["operating\_airline\_iata\_code"].fillna("unknown")

```



Goal: Preserve records while maintaining categorical integrity.



\---



\### 7. Duplicate Removal



```python

df = df.drop\_duplicates()

```



Goal: Ensure each record is unique.



\---



\### 8. Statistical Exploration



```python

df.describe()

```



Goal: Understand distribution and detect anomalies.



\---



\### 9. Outlier Identification



```python

df.sort\_values(by="landing\_count", ascending=False).head()

```



Goal: Identify unusually high activity and validate whether it reflects real operations.



\---



\### 10. Data Validation



Checked for logical consistency across categorical fields and ensured values align with expected domain behavior.



\---



\### 11. Export Clean Dataset



```python

df.to\_csv("datasets/cleaned\_air\_traffic.csv", index=False)

```



Goal: Create a reusable dataset for analysis and reporting.



\---



\## Key Insights



\* A small number of airlines contribute disproportionately to total landing activity

\* Landing counts show strong seasonal patterns, reinforcing the need for year over year comparison

\* Certain aircraft types consistently dominate operational usage

\* Extreme values highlight high traffic routes or hub operations rather than errors



\---



\## Impact



The cleaned dataset is now:



\* Structured and analysis ready

\* Consistent across all fields

\* Reliable for time series comparison

\* Suitable for dashboards, reporting, and further modeling



This reduces data preparation time and improves the quality of insights derived from the dataset.



\---



\## Project Structure



```

project/

│

├── notebooks/

│   └── data\_cleaning.ipynb

│

├── datasets/

│   ├── air\_traffic.csv

│   └── cleaned\_air\_traffic.csv

│

└── README.md

```



\---



\## Tools Used



\* Python

\* pandas

\* Jupyter Notebook



\---



\## Author



Jude Nwagu

Data Professional



