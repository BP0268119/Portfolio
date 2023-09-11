# Predicting Lung Cancer Using Logistic Regression

## Project Overview

In this project, I aimed to develop a predictive model to identify whether a patient would be diagnosed with lung cancer. Lung cancer is the most common cancer death in the UK, with approximately 34,800 deaths every year (Cancer Research UK, 2019). Understanding and predicting the symptoms and lifestyle factors which are strongly linked to lung cancer can help healthcare professionals/institutions to take proactive measures (such as screenings, awareness campaigns, resource allocation, etc.) to prevent lung cancer cases before they occur, and improve cancer patient outcomes through early detection.


## Data Source
The [data](https://github.com/BP0268119/Portfolio/blob/main/Data%20Science%20Project/lung_cancer_data.csv) was a CSV sourced from Kaggle (Nelson, 2022). It contains patient information such as gender, age, their smoking status, whether they consumed alcohol and whether they displayed symptoms such as wheezing, coughing and shortness of breath. 

## Data Processing 

### Data Cleaning 

Prior to any analysis, the data underwent several cleaning stages. These included:

Examining the data

```
raw_data.info()

Data columns (total 16 columns):
 #   Column                 Non-Null Count  Dtype 
---  ------                 --------------  ----- 
 0   GENDER                 309 non-null    object
 1   AGE                    309 non-null    int64 
 2   SMOKING                309 non-null    int64 
 3   YELLOW_FINGERS         309 non-null    int64 
 4   ANXIETY                309 non-null    int64 
 5   PEER_PRESSURE          309 non-null    int64 
 6   CHRONIC DISEASE        309 non-null    int64 
 7   FATIGUE                309 non-null    int64 
 8   ALLERGY                309 non-null    int64 
 9   WHEEZING               309 non-null    int64 
 10  ALCOHOL CONSUMING      309 non-null    int64 
 11  COUGHING               309 non-null    int64 
 12  SHORTNESS OF BREATH    309 non-null    int64 
 13  SWALLOWING DIFFICULTY  309 non-null    int64 
 14  CHEST PAIN             309 non-null    int64 
 15  LUNG_CANCER            309 non-null    object
```

Seeing if there were any missing or null values

```
nan_count = raw_data.isna().sum().sum()
null_count = raw_data.isnull().sum().sum()
total_missing = nan_count + null_count
print('Number of missing values:', total_missing)
Number of missing values: 0
```

De-duplicating any duplicated data

```
raw_data.duplicated().sum()
Out[8]: 33
```

```
data=raw_data.drop_duplicates()
```

Re-examining the data after these steps to see how the data had changed (i.e. how many entries remained)

```
data.info()

<class 'pandas.core.frame.DataFrame'>
Int64Index: 276 entries, 0 to 283
Data columns (total 16 columns):
 #   Column                 Non-Null Count  Dtype 
---  ------                 --------------  ----- 
 0   GENDER                 276 non-null    object
 1   AGE                    276 non-null    int64 
 2   SMOKING                276 non-null    int64 
 3   YELLOW_FINGERS         276 non-null    int64 
 4   ANXIETY                276 non-null    int64 
 5   PEER_PRESSURE          276 non-null    int64 
 6   CHRONIC DISEASE        276 non-null    int64 
 7   FATIGUE                276 non-null    int64 
 8   ALLERGY                276 non-null    int64 
 9   WHEEZING               276 non-null    int64 
 10  ALCOHOL CONSUMING      276 non-null    int64 
 11  COUGHING               276 non-null    int64 
 12  SHORTNESS OF BREATH    276 non-null    int64 
 13  SWALLOWING DIFFICULTY  276 non-null    int64 
 14  CHEST PAIN             276 non-null    int64 
 15  LUNG_CANCER            276 non-null    object
```
