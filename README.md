# Enterprise SaaS Churn Capstone: Adoption & Value Realization

**Author:** Pasupathy Balagurunathan  
**Assignment:** Required Capstone Assignment 20.1 — Initial Report and Exploratory Data Analysis

## Executive summary
This project demonstrates data quality checks, exploratory data analysis, feature engineering and a baseline Logistic Regression workflow for identifying enterprise SaaS accounts at risk of churn or downgrade.

**Data notice:** The committed CSV is synthetic teaching data containing 50 accounts and five churn-positive labels (10%). It is not real customer telemetry. Model metrics are unstable and are not evidence of production predictive performance.

## Business question
Can account profile, product adoption, engagement, executive sponsorship, customer satisfaction and KPI value-realization indicators help identify accounts at risk of churn or downgrade?

## Project contents
- [Initial report](report/Capstone_Initial_Report_EDA.docx)
- [EDA and baseline notebook](notebooks/capstone_eda_baseline.ipynb)
- [Synthetic dataset](data/saas_telemetry.csv)
- [Visualizations](images/)
- [Python dependencies](requirements.txt)

## Methodology
1. Inspect shape, data types, missingness, target balance and duplicate account IDs.
2. Remove duplicate account identifiers; flag numeric outliers using the 1.5×IQR rule. Outliers are not automatically deleted because extreme enterprise values may be legitimate.
3. Engineer ARR per seat, adoption gap and value deficit.
4. Explore class balance, churn by tier, utilization distribution, numeric correlations and CSAT/KPI differences.
5. Fit Logistic Regression with median/mode imputation, scaling and one-hot encoding inside a scikit-learn pipeline.
6. Evaluate recall, precision, Average Precision (PR-AUC), ROC-AUC and confusion matrix.

## Metric rationale
Recall matters because missed churn cases can represent lost recurring revenue. Precision reflects Customer Success intervention workload. Average Precision summarizes the precision-recall trade-off under class imbalance. ROC-AUC is supplementary; accuracy alone is not emphasized.

## Limitations
With only five churn-positive examples, a stratified 25% test split contains very few positive cases. Metrics can change materially with one prediction. Treat this as a coursework workflow demonstration, not a validated churn model. A production study requires a larger governed dataset, time-based validation, leakage controls, calibration, segment evaluation and human review.

## Run locally
```bash
python -m pip install -r requirements.txt
cd notebooks
jupyter notebook capstone_eda_baseline.ipynb
```
