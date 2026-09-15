# early-warning-predictive-maintenance
Source code and supporting materials for an MSc dissertation on early warning HDD failure prediction using S.M.A.R.T. telemetry and a Hybrid LSTM-XGBoost model.

# Early Warning Predictive Maintenance for Enterprise Storage Arrays

## Using Machine Learning-Based Failure Prediction

**Author:** Vishesh Divya  
**Programme:** MSc Data Science  
**University:** Liverpool John Moores University  
**Year:** 2026

---

## Project Overview

This repository contains the source code developed for the MSc dissertation:

**"Early Warning Predictive Maintenance for Enterprise Storage Arrays Using Machine Learning-Based Failure Prediction"**

The research investigates the use of machine learning to predict imminent Hard Disk Drive (HDD) failures using S.M.A.R.T. telemetry.

The study focuses on predicting whether a drive is likely to fail within the following **7 days**, with the objective of investigating whether machine learning can provide an early-warning capability for proactive storage infrastructure management.

---

## Research Approach

The study evaluates five machine-learning approaches:

- Logistic Regression
- Random Forest
- XGBoost
- LSTM
- Hybrid LSTM-XGBoost

The experimental design uses a chronological evaluation:

- **January 2026:** Training
- **February 2026:** Validation
- **March 2026:** Independent held-out testing

---

## Dataset

The research uses the publicly available:

**Backblaze Hard Drive Test Data**

The study uses S.M.A.R.T. telemetry from the Q1 2026 dataset.

Dataset source:

https://www.backblaze.com/cloud-storage/resources/hard-drive-test-data

The complete dataset is not included in this repository because of its size. Users should obtain the original data directly from Backblaze.

---

## Feature Engineering

The modelling framework uses:

- 32 raw S.M.A.R.T. features
- 1-day change features
- 3-day rolling mean
- 7-day rolling mean
- 7-day rolling standard deviation
- 7-day trend

These produce:

**32 raw features + 160 temporal features = 192 structured features**

For temporal modelling, a sequence of **7 observations** is provided to the LSTM.

The LSTM produces a **32-dimensional learned temporal representation**.

The Hybrid model combines:

**192 structured features + 32 LSTM features = 224 features**

---

## Hybrid LSTM-XGBoost Architecture

The proposed Hybrid architecture combines:

1. Structured S.M.A.R.T. and engineered temporal features
2. A 7-observation LSTM temporal representation
3. XGBoost for final classification

The purpose is to investigate whether learned temporal information can complement structured machine-learning features.

---

## Evaluation

The models are evaluated using:

- ROC-AUC
- Average Precision (AP / PR-AUC)
- Precision
- Recall
- F1-score
- Specificity
- False Negative Rate (FNR)

Because HDD failures are extremely rare, the study also evaluates model performance using **fixed alert budgets**.

SHAP-based analysis is used to investigate model behaviour and feature contributions.

---

## Key Result

On the unseen March 2026 held-out cohort, the Hybrid LSTM-XGBoost model achieved:

**ROC-AUC: 0.8662**

**Average Precision: 0.0265**

The Hybrid model also identified more true positives than XGBoost at every tested fixed alert budget.

For example:

| Alert Budget | XGBoost TP | Hybrid TP |
|---:|---:|---:|
| 100 | 2 | 20 |
| 500 | 51 | 63 |
| 1,000 | 70 | 102 |
| 2,500 | 97 | 159 |
| 5,000 | 149 | 241 |
| 10,000 | 218 | 324 |

These results represent the experimental March 2026 cohort and should not be interpreted as universal production thresholds.

---

## Source Code

The main Python implementation is provided in:

`predictive_maintenance.py`

---

## Presentation

A recorded presentation of the dissertation is available here:

**[Presentation Video](ADD-YOUTUBE-LINK-HERE)**

---

## Academic Context

This repository accompanies the MSc Data Science dissertation submitted to:

**Liverpool John Moores University**

**September 2026**

---

## Important Notes

This repository contains the research implementation for the dissertation.

The research does not represent a production deployment of a predictive-maintenance system.

SHAP results describe model behaviour and should not be interpreted as evidence of physical causality.

The findings are based on the Backblaze dataset and the experimental design described in the dissertation.
