# D2C Customer Churn — Part 1: Data Audit, EDA & Business Understanding

## Project Objective

This repository contains Part 1 of the D2C Customer Churn Intelligence & Retention API capstone project.

The objective of this phase is to understand the business problem, audit raw datasets, identify data quality issues, perform exploratory data analysis (EDA), and generate business-backed churn-risk hypotheses before any predictive modeling.

---

## Repository Structure

```text
part1-d2c-data-audit-eda/
│── data/
│   ├── customers.csv
│   ├── orders.csv
│   ├── support_tickets.csv
│   ├── web_events_snapshot.csv
│   ├── churn_labels.csv
│   ├── intervention_history.csv
│
│── eda_audit.ipynb
│
│── outputs/
│   ├── charts/
│   └── joined_dataset_sample.csv
│
│── reports/
│   ├── data_quality_report.md
│   └── business_memo.md
│
│── requirements.txt
│── README.md
│── .gitignore
```

---

## Dataset Used

The following datasets were used:

* customers.csv
* orders.csv
* support_tickets.csv
* web_events_snapshot.csv
* churn_labels.csv
* intervention_history.csv

Primary join key across datasets: `customer_id`

---

## Key Tasks Completed

### 1. Data Loading & Schema Inspection

* Loaded and inspected all raw datasets
* Checked data types, shapes, null values, and schema consistency
* Verified joins using `customer_id`

### 2. Data Quality Audit

Performed checks for:

* Missing values
* Duplicate and duplicate-like records
* Invalid/unusual values
* Outliers
* Join/key issues
* Date consistency
* Potential data leakage risks

### 3. Exploratory Data Analysis (EDA)

Analyzed:

* Customer demographics
* Order behavior
* Monetary behavior
* Support-ticket activity
* Return/refund behavior
* Web/app engagement
* Campaign/intervention history
* Churn distribution

### 4. Churn Risk Hypotheses

Identified churn-risk patterns using dataset-backed visual analysis and business interpretation.

### 5. Business Memo

Created a business-facing memo outlining investigation priorities before launching retention campaigns.

---

## How to Run

### 1. Clone the repository

```bash
git clone <your-github-repo-link>
cd part1-d2c-data-audit-eda
```

### 2. Install dependencies

```bash
pip install -r requirements.txt
```

### 3. Launch notebook

```bash
jupyter notebook
```

Open:

```text
eda_audit.ipynb
```

---

## Important Note

To avoid target leakage, only data available on or before the snapshot date (`2025-09-30`) was considered for feature-related analysis. Post-snapshot orders were analyzed separately and not treated as usable customer behavior signals.
