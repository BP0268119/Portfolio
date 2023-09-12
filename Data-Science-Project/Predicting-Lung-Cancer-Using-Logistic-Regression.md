# Predicting Lung Cancer Using Logistic Regression

## Project Overview

In this project, I aimed to develop a predictive model to identify whether a patient would be diagnosed with lung cancer. Lung cancer is the most common cancer death in the UK, with approximately 34,800 deaths every year (Cancer Research UK, 2019). Understanding and predicting the symptoms and lifestyle factors which are strongly linked to lung cancer can help healthcare professionals/institutions to take proactive measures (such as screenings, awareness campaigns, resource allocation, etc.) to prevent lung cancer cases before they occur, and improve cancer patient outcomes through early detection.


## Data Source
The [data](https://github.com/BP0268119/Portfolio/blob/main/Data-Science-Project/lung-cancer-data.csv) was a CSV sourced from Kaggle (Nelson, 2022). It contains patient information such as gender, age, their smoking status, whether they consumed alcohol and whether they displayed symptoms such as wheezing, coughing and shortness of breath. 

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
## Exploratory Data Analysis (EDA)

Exploratory data analysis was performed to gain an understanding of the dataset (Mukhiya and Ahmed, 2020). The data was all categorical except for age, which was continuous. 

Firstly, the balance of the data was explored. This began with confirming whether there were approximately even numbers of males and females to ensure there wouldn’t be a bias towards gender in the model.

![Gender dist](https://github.com/BP0268119/Portfolio/assets/144491381/3ce76a8a-10b8-497b-a092-bffd741bb0c4)

Then the distribution of the target variable (lung cancer) was assessed. This, again, was necessary to ensure there wouldn’t be a bias present the model. 

![Cancer dist](https://github.com/BP0268119/Portfolio/assets/144491381/48b8bfb1-d501-43f9-b807-804164cd991f)

In this case, there was a large imbalance between those with and without lung cancer. Upon further inspection, approximately 90% of patients had lung cancer and 10% did not. This meant that, without intervention, the model would likely predict most patients to have cancer regardless of any other factors, meaning it would not be very useful and could be harmful if deployed for real patients - i.e., telling a patient they likely have lung cancer when they do not. This result meant that the data would need to undergo further steps to balance the data used to train the model to make sure that the model is robust. 

![Data proportions of cancer yesno](https://github.com/BP0268119/Portfolio/assets/144491381/b0bb6a94-fd3d-44b6-aed7-4462655f6771)

An attempt was made to explore correlations between factors by producing a correlation heatmap. However, this proved ineffective due to the binary nature of the variables used. The graph has still been included to demonstrate this.

![Corr plot](https://github.com/BP0268119/Portfolio/assets/144491381/9181dfc3-3723-4ca4-9cc2-bd66b9a1ed4b)

Then the gender values we re-assigned from M and F to 1 and 2, respectively, as well as the lung cancer values from ‘NO’ and ‘YES’ to 1 and 2, respectively. This was undertaken to normalise these columns so that analysis could be completed.

Next, a heatmap was produced to try to visualise any relationships between variables (Yi, 2020). Instead, this graph highlighted that the ‘age’ variable also needed to be normalised. This is because 'age' is a continuous variable and ranges from 21 to 87, yet all other variables are categorical with a value of either 1 or 2. This could pose an issue as the model could favour features with a wider range of values. As such, they have different ranges and so ‘age’ needed to be rescaled to ensure all the data was using a common scale (Urvashi Jaitley, 2018; Towards AI, 2019).

![heatmap age needs normalising](https://github.com/BP0268119/Portfolio/assets/144491381/a8b7dc82-c5b2-4f77-ac50-ebcb1b1035a7)

Another approach attempted was principal component analysis (PCA). However, again due to the categorical nature of the data, this did not prove useful.

![number of components](https://github.com/BP0268119/Portfolio/assets/144491381/511cad02-c9e6-41ce-b267-f4a53a56455a)

## Model Building and Analysis

### Test/train split

Firstly, the data was split into a training dataset and a test dataset (75% and 25%, respectively).

```
train, test = train_test_split(data_clean, test_size = 0.25, random_state = 42, stratify = data_clean['LUNG_CANCER'])
X_train, y_train, X_test, y_test = train.drop(['LUNG_CANCER'], axis = 1), train['LUNG_CANCER'], \
                                   test.drop(['LUNG_CANCER'], axis = 1), test['LUNG_CANCER']

```

### Normalisation

Then all the data was normalised so that all values would now fall between 0 and 1. As mentioned previously, this was to ensure that all variables were using the same scale to try and eliminate any biases and make the model robust.

```
normalizer = MinMaxScaler()
X_train = pd.DataFrame(normalizer.fit_transform(X_train), columns = X_train.columns)
X_test = pd.DataFrame(normalizer.transform(X_test), columns = X_test.columns)
```

### Baseline Model

Firstly, a very basic model was produced to be used as a baseline, so that subsequent models could be compared to it to see if they perform better or worse. For this, only three variables were chosen: ‘fatigue’, ‘allergy’ and ‘chronic disease’. The performance of this, and all subsequent models, was assessed by a confusion matrix, accuracy, precision, recall, F1 score and AUC. 

The confusion matrix is a summary of how the model has classified the data. One axis of the matrix represents how the model predicted (in this case, whether the patients had cancer or not) and the other axis is the truth of the data. This allows comparison of models by looking at how well they predicted true positives and trye negatives (Silwal, 2022).

Broadly, accuracy defines how correct the model is, precision is how well it classifies the positive predictions, recall is known as sensitivity or the true positive rate, and F1 score is a weighted average of precision and recall, making it more useful than accuracy, especially in the context of imbalanced data (Harikrishnan, 2019; Silwal, 2022).

AUC, or the area under the receiver operating characteristic (ROC) curve, represents the ability of a binary model to discern between the two states. For example, an AUC of 0.5 would mean that the model had no ability to classify data, whereas an AUC of 1.0 would represent perfect prediction (Hoo, Candlish and Teare, 2017).

![baseline conf matrix](https://github.com/BP0268119/Portfolio/assets/144491381/76c73cb5-a429-4f58-bd8f-9e8c76b13f2c)

```
evaluation_metrics_baseline(baseline_Y_test_data, y_pred_baseline)
Accuracy: 0.7971014492753623
Precision: 0.9591836734693877
Recall: 0.7966101694915254
F1-score: 0.8703703703703702
```

![roc baseline](https://github.com/BP0268119/Portfolio/assets/144491381/785a39a9-291b-47dc-a072-479ee5b7d0c7)

### Oversampling

As highlighted previously, the target variable (lung cancer) was highly imbalanced. Therefore, to reduce the risk of an inaccurate model, it was necessary to artificially balance this variable. 

As such, synthetic minority oversampling technique (SMOTE) was chosen. SMOTE generates new data entries by interjecting a point between observations within the data (Chadha, 2021) and so produces more varied data entries than random oversampling, helping to reduce the risk of overfitting and increasing robustness (Bordia, 2022).

### Logistic Regression Model - Balanced Data

This model was trained on the data produced by SMOTE.

![balanced conf matrix](https://github.com/BP0268119/Portfolio/assets/144491381/7540c8e3-de41-4a59-b6e4-59e29aea8319)

```
evaluation_metrics_balanced(y_test, y_pred_balanced)
Accuracy: 0.855072463768116 
Precision: 0.9454545454545454 
Recall: 0.8813559322033898 
F1-score: 0.9122807017543859
```

![roc balanced](https://github.com/BP0268119/Portfolio/assets/144491381/87161acc-c761-40fd-ae62-6845c493facf)

### Logistic Regression Model - Imbalanced Data

It was then thought that it would be pertinent to investigate the performance of a model which was trained using the original imbalanced data (i.e., had not undergone SMOTE). 

![imbalanced conf matrix](https://github.com/BP0268119/Portfolio/assets/144491381/e8d502af-a027-4fd3-a499-2faa1fee2728)

```
evaluation_metrics_imbalanced(y_test, y_pred_imbalanced)
Accuracy: 0.927536231884058 
Precision: 0.9354838709677419 
Recall: 0.9830508474576272 
F1-score: 0.9586776859504132
```

![roc imbalanced](https://github.com/BP0268119/Portfolio/assets/144491381/80de7325-77ff-489d-bd0a-ece2f72c72a4)

### Model Performance
The performance of all three models is be summarised below:

<img width="351" alt="models table" src="https://github.com/BP0268119/Portfolio/assets/144491381/0eb9b32a-63d7-464a-a3a0-a55ddfe3bcaf">

Based on this table and the AUC values, the model based on the imbalanced data has performed the best.

## Insight
As the aim of this project was to discover which factors were the most important in this dataset in relation to developing lung cancer, a feature importance graph was produced based on the best performing model. 

![importance imbalanced](https://github.com/BP0268119/Portfolio/assets/144491381/8025197d-09a5-47ec-a89c-bb506714160c)

The graph shows that the top three important variables were ‘chronic disease’, ‘fatigue’ and ‘allergy’. 

## Recommendations for Future Iterations

This project would benefit from additional data. The source data was quite a small dataset of 309 entries, which reduced to 276 after cleaning and pre-processing. If a larger dataset was used, it would supply more information to the model and improve its accuracy by reducing the likelihood of overfitting (Marshall, 2021). 

Furthermore, additional data would mean that some could be withheld during the train-test splitting and be used for validation at the very end of the modelling process to prevent data leakage (Cook, 2023) and will test whether the model acts as expected for completely unseen data (Tam, 2021).

Another improvement could be to include more variables and use principal component analysis (PCA). PCA is a feature engineering method which aims to reduce the number of dimensions whilst preserving as much information about patterns or relationships between the variables (Goonewardana, 2019). 

Additionally, a better, more statistical approach to comparing models could be taken. For instance, Akaike information criterion (AIC). AIC considers type II errors (false negatives) to be more undesirable than type I (false positives) errors (Banerjee et al., 2009; Randa, 2019). This would be appropriate as the cost of a false positive is gravely different to the cost of a false negative in the context of a cancer prediction (Chawla et al., 2002).



# Conclusion

This project has successfully developed a predictive model for lung cancer using logistic regression, albeit limited. By implementing the above recommendations, the model could be improved and could potentially help to inform healthcare professions and institutions about the most influential factors in developing lung cancer, with a view to aid prevention and improve patient outcomes.
