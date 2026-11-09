## Live Vercel deployment

[Open the deployed project](https://enterprise-saas-churn-capstone-bpasupathy.vercel.app)

# Enterprise SaaS Churn Capstone: Adoption & Value Realization

**Author:** Pasupathy Balagurunathan  
**Assignment:** Required Capstone Assignment 20.1 — Initial Report and Exploratory Data Analysis

## Executive summary
This project demonstrates data-quality assessment, exploratory data analysis, feature engineering and a Logistic Regression baseline for enterprise SaaS churn/downgrade risk.

**Data notice:** The CSV is synthetic teaching data: 50 accounts, five churn-positive labels (10%) and four intentionally missing values. It is not real customer telemetry. Model results are unstable and must not be used for account decisions.

## Project contents
- [Initial report (Markdown)](report/Capstone_Initial_Report_EDA.md)
- [EDA and baseline notebook](notebooks/capstone_eda_baseline.ipynb)
- [Synthetic dataset](data/saas_telemetry.csv)
- [Python dependencies](requirements.txt)
- [Churn distribution chart](images/churn_distribution.svg)
- [Baseline metric chart](images/model_metrics.svg)

## Methodology
1. Inspect dimensions, missingness, target balance and duplicate account IDs; remove duplicate identifiers.
2. Flag numeric outliers with the 1.5×IQR rule. Do not automatically delete plausible enterprise-scale values.
3. Engineer ARR per seat, adoption gap and value deficit.
4. Explore churn balance, churn by tier, utilization, numeric correlations and CSAT/KPI differences.
5. Fit Logistic Regression with median/mode imputation, scaling and one-hot encoding inside a scikit-learn pipeline.
6. Evaluate recall, precision, Average Precision (PR-AUC), ROC-AUC and confusion matrix.

## Baseline results
On the stratified holdout test set: recall 0.000, precision 0.000, PR-AUC 0.200 and ROC-AUC 0.667. The test set contains only one churn-positive example; these metrics are highly unstable. The classifier did not detect that positive case.

Recall is emphasized because missed churn cases may expose recurring revenue to loss. Precision reflects Customer Success intervention workload. Average Precision summarizes the precision-recall trade-off under class imbalance.

## Limitations and next steps
This is a coursework workflow demonstration, not a validated churn model. A production study requires a larger governed dataset, an observation window preceding the renewal outcome, time-based validation, leakage controls, calibration, segment evaluation and human review.

## Run locally
```bash
python -m pip install -r requirements.txt
cd notebooks
jupyter notebook capstone_eda_baseline.ipynb
```
