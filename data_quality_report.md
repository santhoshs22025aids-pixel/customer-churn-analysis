# Data Quality and Exploratory Analysis — Customer Churn

## 1. Decision question
Which customer groups should a fictional subscription team contact first to reduce avoidable churn?

## 2. Dataset scope
- Source: supplied synthetic customer churn CSV.
- Rows: **15** customers.
- Columns: **11**.
- Data is synthetic; findings are descriptive and should not be treated as causal or generalizable.
- Note: the supplied guide describes a smaller set of fields, while the actual CSV contains 11 columns. This analysis follows the actual CSV schema.

## 3. Quality audit and cleaning decisions

| Check | Result | Decision |
|---|---:|---|
| Missing values | 0 cells missing | No imputation required. |
| Exact duplicate rows | 0 | No rows removed. |
| Duplicate customer IDs | 0 | No IDs removed. |
| Invalid ages outside 0–120 | 0 | No age corrections needed. |
| Negative tenure | 0 | No corrections needed. |
| Negative monthly charges | 0 | No corrections needed. |
| Negative total charges | 0 | No corrections needed. |
| Negative support-ticket counts | 0 | No corrections needed. |
| Churn values outside Yes/No | 0 | No corrections needed. |
| Contract labels outside expected set | 0 | No corrections needed. |
| TotalCharges mismatch vs TenureMonths × MonthlyCharges (> INR 0.02 tolerance) | 0 | All rows match the apparent sample calculation within tolerance. |

**Cleaning performed:** trimmed surrounding whitespace from column names and text fields; explicitly converted the numeric columns to numeric types; saved a cleaned CSV. No records were deleted because no row-level defect requiring deletion was identified.

### Outlier screening
IQR screening was applied to numeric fields. IQR flags are a review aid, not proof of bad data. Values were retained rather than deleted automatically.

| Numeric field | IQR lower bound | IQR upper bound | Flagged values |
|---|---:|---:|---|
| Age | 4.50 | 72.50 | 0 |
| TenureMonths | -23.00 | 57.00 | 0 |
| MonthlyCharges | -47.51 | 212.49 | 0 |
| TotalCharges | -3689.82 | 7349.46 | 0 |
| SupportTickets | -3.50 | 8.50 | 0 |

## 4. Summary statistics

| Metric | Value |
|---|---:|
| Customers | 15 |
| Churned customers | 7 |
| Observed churn rate | 46.7% |
| Average age | 39.1 years |
| Median tenure | 15.0 months |
| Average monthly charge | INR 84.66 |
| Median total charges | INR 1099.78 |
| Average support tickets | 2.53 |

## 5. Initial patterns

### Churn by contract type
| ContractType   |   customers |   churned |   churn_rate_pct |
|:---------------|------------:|----------:|-----------------:|
| Month-to-Month |           7 |         7 |              100 |
| One Year       |           4 |         0 |                0 |
| Two Year       |           4 |         0 |                0 |

All 7 Month-to-Month customers in this small sample churned, while none of the fixed-term contract customers did. This is a strong pattern in this sample, but it is based on only 15 rows and should be verified on a larger dataset.

### Churn by subscription type
| SubscriptionType   |   customers |   churned |   churn_rate_pct |
|:-------------------|------------:|----------:|-----------------:|
| Basic              |           7 |         5 |             71.4 |
| Enterprise         |           4 |         0 |              0   |
| Pro                |           4 |         2 |             50   |

The Basic tier has the highest observed churn rate (71.4%). The group sizes are small, so the rates are unstable.

### Churn by payment method
| PaymentMethod   |   customers |   churned |   churn_rate_pct |
|:----------------|------------:|----------:|-----------------:|
| Bank Transfer   |           3 |         0 |              0   |
| Credit Card     |           6 |         2 |             33.3 |
| Debit Card      |           2 |         2 |            100   |
| UPI             |           4 |         3 |             75   |

Payment-method differences may be worth checking, but they may reflect other factors (such as contract type or tenure) rather than a direct relationship.

### Visuals
- `churn_counts.png`: count of customers by churn status.
- `churn_by_contract.png`: observed churn rate by contract type.
- `churn_by_subscription.png`: observed churn rate by subscription type.

## 6. Recommendation
**Audience:** Start by reviewing Month-to-Month customers, particularly Basic-tier customers with multiple recent support tickets.  
**Decision:** Pilot a proactive retention check-in that asks about service issues and offers appropriate plan information; do not assume that changing a contract alone will prevent churn.  
**Supporting metrics:** 7/7 Month-to-Month customers churned in this sample; 5/7 Basic customers churned; the overall observed churn rate is 46.7%.  
**Uncertainty:** The sample has only 15 synthetic records, is not necessarily representative, and the observed associations do not establish causation. The apparent relationship between tenure and charges is also built into the sample's charge calculation.  
**Next measurement:** Track contacted vs. non-contacted eligible customers over a defined period, and compare subsequent churn rate, support-ticket volume, and retention cost. If feasible, use a randomized pilot or a matched comparison group.

## 7. Limitations
1. Small synthetic sample; percentages can change substantially with a few customers.
2. No observation dates, customer acquisition channel, reasons for churn, or intervention outcomes are provided; no causal conclusions can be made.

## 8. Reproducibility
Run `analysis.ipynb` from top to bottom in Jupyter Notebook or Google Colab. The notebook loads `customer_churn_sample.csv`, runs quality checks, creates the cleaned dataset, summary tables, and charts. The included cleaned CSV and report reflect the supplied sample.
