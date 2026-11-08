# Enterprise SaaS Churn Capstone: Adoption & Value Realization

**Author:** Project starter  
**Primary notebook:** [capstone_eda_baseline.ipynb](notebooks/capstone_eda_baseline.ipynb)

## Executive summary

This project demonstrates an end-to-end exploratory data analysis and baseline machine-learning workflow for identifying enterprise SaaS accounts at risk of churn or downgrade. It combines account profile, license utilization, engagement, product breadth, executive sponsorship, customer satisfaction, and KPI value realization.

**Data disclaimer:** The included `saas_telemetry.csv` is a deterministic synthetic/mock dataset of 12,000 generated account records. It is not real customer telemetry and should not be used for real account-level decisions. It is provided so the project is immediately reproducible while approved data access is pending.

## Rationale

For high-value SaaS contracts, failing to identify an account that later churns can result in significant recurring-revenue loss. False positives also have a cost because Customer Success teams have limited capacity, but proactive outreach to a healthy account is generally less costly than missing a genuine churn risk. This motivates recall and precision-recall metrics rather than accuracy alone.

## Research question

Can account profile, adoption and usage signals, and value-realization indicators predict the `churn` label (1 = churned/downgraded; 0 = renewed) early enough to support targeted Customer Success intervention?

## Data sources

The repository includes a synthetic dataset at `data/saas_telemetry.csv` with 12,000 rows and 18 source fields. It covers:

- Account profile: account ID, contract tenure, tier, ARR, and licensed seats.
- Adoption and usage: license utilization, DAU/MAU ratio, active core modules, and API call volume.
- Value realization: KPI milestones achieved, automated workflows, executive sponsor QBR attendance, and CSAT.
- Target: churn / downgrade indicator.

For a production version, replace the mock file with approved, de-identified CRM, product telemetry, renewal, and customer-success data. Document data owners, extraction windows, label definitions, and privacy controls.

## Methodology

1. **Data quality:** inspect dimensions, data types, missingness, duplicates, and target balance.
2. **Feature engineering:** derive `arr_per_seat`, `adoption_gap`, and `value_deficit`.
3. **EDA:** compare churn prevalence by tier and utilization band; inspect utilization, CSAT, and KPI milestone distributions by outcome.
4. **Baseline model:** Logistic Regression in a scikit-learn Pipeline, with numeric imputation and `StandardScaler`, plus categorical imputation and `OneHotEncoder`.
5. **Validation:** stratified 75/25 train/test split, fixed random seed, and balanced class weights. The initial operating threshold is 0.5.
6. **Evaluation:** recall and Average Precision (PR-AUC) are primary; precision and ROC-AUC are supplementary. Confusion matrix, precision-recall curve, and coefficients support interpretation.

## Results: EDA findings

The synthetic dataset has an overall churn prevalence of **16.8%**. Descriptive churn rates are:

| Segment | Churn rate |
|---|---:|
| Enterprise | 11.2% |
| Mid-Market | 20.2% |
| License utilization below 40% | 27.7% |
| License utilization 40–60% | 20.7% |
| License utilization 60–80% | 15.9% |
| License utilization above 80% | 14.1% |

In this generated sample, lower license utilization aligns with higher churn prevalence. Churn-labeled accounts also show lower average engagement, module adoption, KPI achievement, and QBR attendance. These are descriptive patterns intentionally represented in synthetic data, not findings about any actual SaaS population.

### EDA visuals

- [Churn by adoption and tier](images/churn_by_adoption.png)
- [Adoption and value signals by churn](images/adoption_value_signals.png)

## Baseline model results

On the stratified held-out test partition, the Logistic Regression baseline produced:

| Metric | Test score |
|---|---:|
| Recall | 0.685 |
| Precision | 0.279 |
| PR-AUC (Average Precision) | 0.333 |
| ROC-AUC | 0.706 |

Recall is prioritized because false negatives represent missed churn/downgrade accounts. Precision is included to quantify the likely volume of unnecessary interventions. PR-AUC summarizes the precision-recall trade-off under class imbalance. Scores depend on the synthetic data generation process, split, and default threshold; they are not evidence of expected performance on real customer data.

- [Confusion matrix](images/baseline_confusion_matrix.png)
- [Precision-recall curve](images/precision_recall_curve.png)
- [Largest logistic coefficients](images/logistic_coefficients.png)

## Recommendations and next steps

1. Replace mock data with approved account-level telemetry and a clearly governed churn/downgrade label.
2. Use an observation window that ends before the renewal outcome; prevent label leakage from post-churn signals.
3. Move from random splitting to time-based validation to reflect real deployment.
4. Select an operating threshold based on ARR at risk, recall targets, precision, and Customer Success team capacity.
5. Evaluate calibration and performance across Enterprise/Mid-Market tiers, ARR bands, regions, and tenure cohorts.
6. Add trend features such as declining DAU/MAU, utilization changes, support escalations, and renewal proximity.
7. Run a controlled pilot with human review before integrating risk scores into account workflows.

## Outline of project

- [Primary notebook: cleaning, EDA, feature engineering, and baseline ML](notebooks/capstone_eda_baseline.ipynb)
- [Synthetic telemetry dataset](data/saas_telemetry.csv)
- [Images and plots](images/)

## Repository structure

```text
enterprise-saas-churn-capstone/
├── README.md
├── data/
│   └── saas_telemetry.csv
├── notebooks/
│   └── capstone_eda_baseline.ipynb
├── images/
│   ├── churn_by_adoption.png
│   ├── adoption_value_signals.png
│   ├── baseline_confusion_matrix.png
│   ├── precision_recall_curve.png
│   └── logistic_coefficients.png
└── requirements.txt
```

## Run locally

```bash
python -m pip install -r requirements.txt
jupyter notebook notebooks/capstone_eda_baseline.ipynb
```

## Contact and further information

Update this section with the project owner's preferred contact details before external publication.
