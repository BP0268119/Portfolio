# Executive Summary

This project aimed to develop a predictive model using logistic regression to anticipate whether an individual would develop lung cancer based on relevant clinical and demographic features. 

## Problem

In the UK, there are around 34,800 lung cancer deaths every year – approximately 95 per day. Lung cancer is the most common cancer death in the UK, accounting for 21% of all cancer deaths. It is also estimated that 79% of lung cancer cases in the UK are preventable (Cancer Research UK, 2019).  

However, earlier detection could improve patient outcomes (Koo et al., 2019). Cancer is described in stages, from a scale of one to four, where higher the number, the more advanced the cancer is (National Cancer Institute, 2022). In 2020, the majority (51%) of lung cancers in England were diagnosed at stage four. Being diagnosed at this late stage provides a poor prognosis for the patient, with 21.7% surviving one-year post-diagnosis, whilst only 4.3% survive five years. In contrast, patients diagnosed at stage one have a 90.2% one-year survival rate, a 62.7% five-year survival rate, and a 29.0% chance of a ten-year survival (Cancer Research UK, 2022).

By utilising an open-source dataset and applying statistical techniques, this project sought to provide a tool which could potentially be further developed to help healthcare professionals to identify high-risk patients, promote early intervention and tailor screening and prevention strategies accordingly.

## Methods

### The dataset used can be found [here](https://github.com/BP0268119/Portfolio/blob/main/Data-Science-Project/lung-cancer-data.csv).

•	Data collection: 
The dataset used was sourced from Kaggle. It contained selected clinical and demographical information of patients, such as age, smoking history, and alcohol consumption. 

•	Data processing and exploratory analysis: 
The data was uploaded to a Databricks notebook (Python) where it was examined for any missing or null values, or any duplicated entries. Then, the shape and distribution of the data was assessed, and normalisation was applied where necessary. These steps were completed to ensure the data quality and compatibility for model training.

•	Feature selection:
Relevant features were identified using feature importance analysis and correlation analysis to enhance model performance and reduce dimensionality.

•	Model Development: 
Logistic regression, a well-established statistical technique for binary classification, was used to build the predictive model. 

•	Model Evaluation: 
The model was evaluated using metrics such as accuracy, precision, recall, F1-score, and ROC-AUC to assess its performance.


## Outcomes

•	A logistic regression model with a high predictive accuracy for lung cancer

•	Insights into the most significant factors influencing lung cancer risk


## Impact

Although this project is not at the scale or robustness necessary for any real-world impact, theoretically, it could several significant impacts if further developed:

•	Early identification of individuals at high risk for lung cancer, allowing for proactive screening and preventive measures

•	Improved patient outcomes due to timely interventions, which can lead to better treatment outcomes and potentially save lives

•	Healthcare resources (e.g., funding, practitioners, equipment) could be allocated more efficiently by focusing on high-risk populations

## Future Directions

Future work may involve expanding the model's scope to include more diverse data sources, refining feature engineering techniques, and integrating advanced machine learning methods to improve prediction accuracy further. Additionally, ongoing data collection and model retraining will be necessary to ensure continued relevance and effectiveness.

## Summary

In conclusion, his project sought to develop a logistic regression model for predicting lung cancer diagnoses, contributing to early detection, improved patient outcomes, and more efficient healthcare resource allocation in the fight against this devastating disease.
