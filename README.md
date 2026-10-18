# Data Analytics Task 1 — Data Quality and Exploratory Analysis

This project audits a supplied synthetic customer churn dataset and explores initial churn patterns.

## Files
- `analysis.ipynb` — reproducible analysis notebook.
- `customer_churn_sample.csv` — original input data.
- `customer_churn_cleaned.csv` — cleaned, analysis-ready data.
- `data_quality_report.md` — quality decisions, metrics, findings, limitations, and recommendation.
- `data_dictionary.csv` — column definitions and quality rules.
- `churn_counts.png`, `churn_by_contract.png`, `churn_by_subscription.png` — visual summaries.

## Main findings
- 15 customers; 7 churned; observed churn rate 46.7%.
- All 7 Month-to-Month customers churned in this sample; no fixed-term customers churned.
- 5 of 7 Basic-tier customers churned (71.4%).
- The sample is small and synthetic. These associations do not establish causation.

## Run
Keep `customer_churn_sample.csv` in the same folder as `analysis.ipynb`, then run all notebook cells in Jupyter or Google Colab.

## Submission
Upload this folder to a public GitHub repository or a view-only Google Drive folder. Submit that single link. Ensure access is set so the reviewer does not need to request permission.
