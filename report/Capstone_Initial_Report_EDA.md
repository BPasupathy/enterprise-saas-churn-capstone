> **Live project page:** [Enterprise SaaS Churn Capstone on Vercel](https://enterprise-saas-churn-capstone.vercel.app)

# Enterprise SaaS Churn Capstone
## Required Capstone Assignment 20.1 — Initial Report and Exploratory Data Analysis

**Author:** Pasupathy Balagurunathan

## Executive summary
This project demonstrates data-quality assessment, exploratory data analysis, feature engineering and a Logistic Regression baseline for identifying enterprise SaaS accounts at risk of churn or downgrade. The supplied data is synthetic: 50 accounts, 16 columns, five churn-positive records (10%) and four intentionally missing values. It is not real customer telemetry.

## Business problem and research question
Churn and downgrade can reduce recurring revenue and customer lifetime value. The analysis asks whether account profile, product adoption, engagement, executive sponsorship, customer satisfaction and KPI value-realization signals can help distinguish churned/downgraded accounts from retained accounts.

## Dataset
The dataset contains account profile (industry, region, tier, tenure, ARR, licensed seats), adoption and usage (license utilization, DAU/MAU, active modules, API calls), value realization (KPI milestones, automated workflows, QBR attendance, CSAT) and the churn target. Four values are missing. These are handled through model-pipeline imputation.

## Data preparation and feature engineering
Duplicate account IDs are checked and removed before analysis. Numeric outliers are flagged with the 1.5×IQR rule; they are not automatically deleted because unusually high ARR, seat counts or usage may be valid for enterprise customers. Derived features include ARR per seat, adoption gap (1 − utilization) and value deficit (1 − KPI milestone attainment). Account ID and target are excluded from predictors.

## Exploratory data analysis
The notebook examines churn class balance, churn by tier, license-utilization distribution, numeric feature correlations and CSAT/KPI differences by churn outcome. These are descriptive associations, not causal findings. With only five positive cases, subgroup rates are unstable.

## Baseline modeling
A Logistic Regression classifier is trained using a stratified 75/25 holdout split. Numeric predictors use median imputation and standardization; categorical predictors use most-frequent imputation and one-hot encoding. Preprocessing is fitted within a scikit-learn pipeline on the training partition. Balanced class weights are used to address class imbalance.

Recall is emphasized because missed churn accounts may represent lost recurring revenue. Precision reflects Customer Success intervention workload. Average Precision (PR-AUC) summarizes the precision-recall trade-off under class imbalance; ROC-AUC is supplementary.

## Results and limitations
The held-out test set contains only one churn-positive example. The executed baseline produced:
- Recall: 0.000
- Precision: 0.000
- PR-AUC (Average Precision): 0.200
- ROC-AUC: 0.667

The model did not identify the single churn-positive test example. With only five positive labels in the full dataset, these metrics are extremely sensitive to individual predictions and cannot establish predictive validity. Treat this as a coursework workflow demonstration, not a deployable churn model.

## Recommendations
1. Replace synthetic data with approved, de-identified CRM, telemetry, renewal and customer-success data.
2. Define an observation window ending before the renewal outcome and prevent post-outcome leakage.
3. Use time-based validation on a substantially larger sample.
4. Select alert thresholds using ARR at risk, recall objectives and Customer Success capacity.
5. Evaluate calibration and performance across tiers, ARR bands, regions and tenure cohorts.
6. Pilot with human review before operational deployment.

## Project links
- [GitHub repository](https://github.com/BPasupathy/enterprise-saas-churn-capstone)
- [Notebook](../notebooks/capstone_eda_baseline.ipynb)
- [Dataset](../data/saas_telemetry.csv)
- [Requirements](../requirements.txt)
