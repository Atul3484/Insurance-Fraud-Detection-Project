# Insurance Fraud Detection Project

## Overview

This project aims to analyze and detect fraudulent insurance claims using real-world structured data. It involves detailed data cleaning, feature engineering, and the application of advanced machine learning techniques to build and evaluate fraud prediction models.

## Contents

- [Introduction](#introduction)
- [Dataset](#dataset)
- [Data Preprocessing](#data-preprocessing)
- [Feature Engineering](#feature-engineering)
- [Exploratory Data Analysis (EDA)](#exploratory-data-analysis-eda)
- [Modeling and Evaluation](#modeling-and-evaluation)
- [Results](#results)
- [Key Features Used](#key-features-used)
- [Usage](#usage)
- [Contact](#contact)

## Introduction

Insurance fraud costs companies billions. Timely detection is vital for reducing losses and maintaining fair practices. This repository demonstrates an end-to-end approach to identifying potentially fraudulent claims using Python and key data science libraries.

## Dataset

The dataset contains 990 insurance claims, including customer, policy, incident, vehicle, and claim details. Each record is labeled as "fraudulent" or "non-fraudulent".

**Features include:**
- Customer demographics (age, sex, education)
- Policy details (dates, deductibles, coverage)
- Incident details (type, severity, location, date)
- Claim amounts (total, injury, property, vehicle)
- Vehicle and auto specs

A target column (`fraud_reported`) indicates if the claim is fraudulent. There is no missing data in the main features, except for some categorical fields, which were handled during preprocessing.

## Data Preprocessing

- Checked for and handled missing values (e.g., filled missing `authorities_contacted` values as "Missing"[1]).
- Verified that there were no blanks or nulls in critical fields.
- Dropped irrelevant columns (e.g., policy number, zip code, raw date columns, and unique locations) to prevent overfitting.
- Converted categorical columns to numeric using one-hot encoding for modeling.
- Addressed class imbalance with **SMOTE** oversampling on the training data.

## Feature Engineering

Added new features to improve predictive power:

- **Days Since Policy Bind:** Days between policy start and incident date.
- **Multi-Vehicle Incident:** Flag for multiple vehicles involved.
- **Month Difference:** The difference in months between binding and incident date.
- Extracted **day of week** and **month** from incident date.
- **Proportional Claim Amounts:** Percent of injury, property, and vehicle claims over total claim.
- Cleaned and standardized umbrella limit values.

## Exploratory Data Analysis (EDA)

- Distribution plots and boxplots for all major numerical features.
- Count plots for categorical variables vs. fraud status.
- Correlation heatmaps identified relationships between features.
- Compared distributions for fraudulent and non-fraudulent classes.
- Feature importance visualized after model training.

## Modeling and Evaluation

Three main machine learning models were trained, evaluated, and compared:

- **Logistic Regression**
- **Random Forest (with GridSearchCV hyperparameter tuning)**
- **XGBoost**

**Model Training:**
- Used stratified train-test split (80/20) to ensure class balance.
- All numeric features were scaled for logistic regression.
- Class imbalance in training data handled with SMOTE; test data remained real/unbalanced for fair evaluation.

**Stacking Ensemble:**
- Combined the above models via stacked generalization (meta-model with logistic regression) for potentially improved prediction.

**Evaluation Metrics:**
- Confusion matrix
- Precision, recall, F1-score
- Accuracy

**Best Results:**
- Logistic Regression achieved ~79% accuracy, best F1 for fraud class at a threshold of 0.2.
- Random Forest and XGBoost were also tested and compared.
- Model threshold tuning was performed to optimize recall (important for flagging more fraud).

## Results

- **Logistic Regression:**  
  - Precision: 0.60 (fraud); Recall: 0.49; F1: 0.54; Accuracy: 79.3%
- **Random Forest (Best Params):**  
  - Precision: 0.36 (fraud); Recall: 0.16; F1: 0.23; Accuracy: 73.2%
- **XGBoost:**  
  - Precision: 0.52 (fraud); Recall: 0.53; F1: 0.53; Accuracy: 76.3%
- **Stacked Ensemble:**  
  - F1 (fraud): 0.64 at threshold 0.2; Accuracy: 80%

## Key Features Used

- Incident severity and type
- Claims breakdown (injury, vehicle, property, total claim)
- Incident state and city
- Months as customer, month difference, days since policy, etc.
- Multi-vehicle involvement flag
- Vehicle characteristics: make/model/year
- Policy deductible and umbrella limit

**Top features by importance:**  
Incident severity, incident state, specific claim amounts, month difference, high policy coverage limits.

## Usage

1. **Data Preparation:**  
   Clean and preprocess data as per the notebook steps.

2. **Training:**  
   - Use provided scripts to train logistic regression, random forest, and XGBoost models.
   - Perform SMOTE only on training data.

3. **Prediction:**  
   - Use `predict()` function of chosen model on new/real test data.

4. **Threshold Tuning:**  
   - Adjust score threshold (recommended: 0.2 to maximize fraud recall).

## Contact

If you have questions or want to contribute, please open an issue or contact the author via email or GitHub.

**Note:**  
The workflow and code are fully reproducible. All results, figures, and feature importances can be regenerated from the supplied notebooks and scripts. This project strives for transparency and practical insight into fraud detection challenges and solutions in insurance[1].

[1] https://ppl-ai-file-upload.s3.amazonaws.com/web/direct-files/attachments/43744170/df6631f8-1f95-4671-ad79-22e72a15c508/fruad-detection-final.pdf
[2] https://ppl-ai-file-upload.s3.amazonaws.com/web/direct-files/attachments/43744170/59685de1-4beb-4c1b-9250-2cb0c4eb4925/Insuarance-Fraud-Detection-Analysis.pdf
[3] https://ppl-ai-file-upload.s3.amazonaws.com/web/direct-files/attachments/43744170/2b437e3f-309a-4f94-bc08-58f0c561f81e/insurance_claims-1.csv
