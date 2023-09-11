# Predicting Lung Cancer Using Logistic Regression

## Project Overview

In this project, I aimed to develop a predictive model to identify whether a patient would be diagnosed with lung cancer. Lung cancer is the most common cancer death in the UK, with approximately 34,800 deaths every year (Cancer Research UK, 2019). Understanding and predicting the symptoms and lifestyle factors which are strongly linked to lung cancer can help healthcare professionals/institutions to take proactive measures (such as screenings, awareness campaigns, resource allocation, etc.) to prevent lung cancer cases before they occur, and improve cancer patient outcomes through early detection.


## Data Source
The [data](https://github.com/BP0268119/Portfolio/blob/main/Data%20Science%20Project/lung_cancer_data.csv) was a CSV sourced from Kaggle (Nelson, 2022). It contains patient information such as gender, age, their smoking status, whether they consumed alcohol and whether they displayed symptoms such as wheezing, coughing and shortness of breath. 

## Data Processing 

The CSV was uploaded to a Databricks notebook and was used to create a pandas dataframe. Python was used for this project.

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
### Exploratory Data Analysis (EDA)

Exploratory data analysis was performed to gain an understanding of the dataset (Mukhiya and Ahmed, 2020). The data was all categorical with the exception of age, which was continuous. 

Firstly, the balance of the data was explored. This began with confirming whether there were approximately even numbers of males and females to ensure there wouldn’t be a bias towards gender in the model.

![Gender dist](https://github.com/BP0268119/Portfolio/assets/144491381/3ce76a8a-10b8-497b-a092-bffd741bb0c4)

Then the distribution of the target variable (lung cancer) was assessed. This, again, was necessary to ensure there wouldn’t be a bias present the model. 

![Cancer dist](https://github.com/BP0268119/Portfolio/assets/144491381/48b8bfb1-d501-43f9-b807-804164cd991f)

In this case, there was a large imbalance between those with and without lung cancer. Upon further inspection, approximately 90% of patients had lung cancer and 10% did not. This meant that, without intervention, the model would likely predict most patients to have cancer regardless of any other factors, meaning it would not be very useful. This result meant that the data would need to undergo further steps to balance the data used to train the model to make sure that the model is robust. 

![Data proportions of cancer yesno](https://github.com/BP0268119/Portfolio/assets/144491381/b0bb6a94-fd3d-44b6-aed7-4462655f6771)

An attempt was made to explore correlations between factors by producing a correlation heatmap. However, this proved ineffective due to the binary nature of the variables used. The graph has still been included to demonstrate this.

![Corr plot](https://github.com/BP0268119/Portfolio/assets/144491381/9181dfc3-3723-4ca4-9cc2-bd66b9a1ed4b)

Then the gender values we re-assigned from M and F to 1 and 2, respectively, as well as the lung cancer values from ‘NO’ and ‘YES’ to 1 and 2, respectively. This was undertaken to normalise these columns so that analysis could be completed.

Next, a heatmap was produced to try to visualise any relationships between variables (Yi, 2020). Instead, this graph highlighted that the ‘age’ variable also needed to be normalised. This is because 'age' is a continuous variable and ranges from 21 to 87, yet all other variables are categorical with a value of either 1 or 2. As such, they have different ranges and so ‘age’ needed to be rescaled to ensure all the data was using a common scale (Urvashi Jaitley, 2018; Towards AI, 2019).

![heatmap age needs normalising](https://github.com/BP0268119/Portfolio/assets/144491381/a8b7dc82-c5b2-4f77-ac50-ebcb1b1035a7)

