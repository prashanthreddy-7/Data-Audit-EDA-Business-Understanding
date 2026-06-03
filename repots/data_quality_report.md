# Data Quality Report

## Overview

This report summarizes the data quality issues identified during exploratory analysis of the D2C customer churn datasets. The objective was to identify missing values, duplicate-like records, outliers, join issues, date inconsistencies, and potential leakage risks that may affect downstream analysis or predictive modeling.

---

## 1. Missing Values

### Customers Dataset

* `loyalty_tier` contains missing values. This likely indicates customers who are not enrolled in the loyalty program rather than missing system data.
* `skin_type` contains missing values, likely due to customers not providing optional profile information.

### Orders Dataset

* `rating` contains missing values, indicating customers who did not leave feedback after purchase.

### Recommendation

* Treat missing `loyalty_tier` as **"Not Enrolled"** rather than removing rows.
* Keep missing `skin_type` as **"Unknown"** or retain null values depending on analysis needs.
* Compute rating-based metrics carefully to avoid bias from null ratings.

---

## 2. Duplicate-Like Records

The `orders.csv` dataset contains intentional duplicate-like records where some `order_id` values end with `_DUP`.

These records simulate real-world duplicate entry challenges and require validation before modeling.

### Recommendation

* Investigate whether `_DUP` records represent true duplicate transactions or replicated entries.
* Avoid blindly dropping records without checking business meaning.

---

## 3. Invalid or Unusual Values

The following checks were performed:

* Invalid order ratings
* Negative or unusual monetary values
* Delivery time anomalies
* Sentiment score range validation

### Findings

* Ratings are expected within the 1–5 range.
* Sentiment scores are expected within -1 to +1.
* Delivery days should remain within realistic operational limits.

### Recommendation

* Flag invalid values for business review if detected.
* Apply validation rules before feature engineering.

---

## 4. Outlier Analysis

Outliers were identified in the `gross_amount` column within the orders dataset.

A small number of unusually high-value transactions were observed.

### Business Interpretation

These may represent:

* Premium customer purchases
* Bulk orders
* Data-entry anomalies

### Recommendation

* Investigate extreme spending behavior before removing outliers.
* Consider winsorization or capping only if justified for modeling.

---

## 5. Join and Key Issues

Datasets were joined using `customer_id`.

### Findings

* `customers.csv` was treated as the base table.
* Not all customers have support tickets, which is expected behavior and not a join issue.
* Left joins preserve the full customer population.

### Recommendation

* Maintain customer-level universe through left joins.
* Avoid inner joins that may unintentionally exclude customers.

---

## 6. Date Consistency Checks

The project uses a snapshot date of `2025-09-30`.

### Findings

* Snapshot datasets consistently use `2025-09-30`.
* Orders include transactions after the snapshot date.

### Recommendation

Validate temporal consistency before analysis to avoid using future information.

---

## 7. Data Leakage Risk (Critical)

`orders.csv` contains post-snapshot orders after `2025-09-30`.

These records exist for churn label generation and must not be used as model features.

### Recommendation

Only use information available on or before the snapshot date for feature engineering and churn analysis.

---

## Conclusion

Overall, the datasets are structurally consistent and suitable for analysis. However, careful handling of missing values, duplicate-like order records, outliers, and post-snapshot leakage is required to ensure reliable business insights and future modeling performance.
