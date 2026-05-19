# Part 1: Data Audit, EDA & Business Understanding
## D2C Customer Churn Intelligence & Retention API — Capstone

---

## Overview

This repository contains Part 1 of the D2C Customer Churn Capstone project.

The objective is to audit raw customer data, perform exploratory analysis, identify data-quality issues, and convert observations into actionable churn-risk business hypotheses.

---

## Repository Structure

```
churn-part1-eda/
│
├── eda_audit.ipynb           ← Main analysis notebook
├── data_quality_report.md    ← Data quality findings and recommendations
├── business_memo.md          ← Business-facing memo for retention strategy
├── requirements.txt          ← Python dependencies
├── charts/                   ← All saved chart outputs (8 charts)
│   ├── chart1_churn_distribution.png
│   ├── chart2_demographics_churn.png
│   ├── chart3_order_behaviour.png
│   ├── chart4_support_tickets.png
│   ├── chart5_app_engagement.png
│   ├── chart6_revenue_analysis.png
│   ├── chart7_correlation_heatmap.png
│   └── chart8_return_behaviour.png
└── README.md
```

---

## Dataset

The dataset package is available here:  
[Google Drive Dataset Link](https://drive.google.com/drive/folders/1PmLapJI1VSDgvl_AxARNKwM1MCd3WFX0?usp=sharing)

Download and place all CSV files in a `data/` folder in the root of this repository before running the notebook.

**Files required in `data/`:**
- `customers.csv`
- `orders.csv`
- `support_tickets.csv`
- `web_events_snapshot.csv`
- `churn_labels.csv`
- `intervention_history.csv`

---

## Setup Instructions

```bash
# 1. Clone the repository
git clone https://github.com/YOUR_USERNAME/churn-part1-eda.git
cd churn-part1-eda

# 2. Create and activate virtual environment
python -m venv venv
venv\Scripts\activate        # Windows
source venv/bin/activate     # Mac/Linux

# 3. Install dependencies
pip install -r requirements.txt

# 4. Download dataset and place CSVs in data/ folder

# 5. Launch Jupyter and run the notebook
jupyter notebook eda_audit.ipynb
```

---

## Key Findings

| Metric | Not Churned | Churned |
|---|---|---|
| Churn Rate | 53% | 47% |
| Avg Orders | 3.70 | 3.04 |
| Avg Revenue | ₹2,839 | ₹2,222 |
| Avg Sessions (30d) | 6.73 | 4.02 |
| Avg Days Since Last Visit | 9.77 | 26.55 |
| Avg Returns | 0.23 | 0.22 |

**Top churn-risk signals identified:**
1. Low purchase frequency (< 3 orders)
2. High days since last app visit (> 14 days)
3. Low session count in last 30 days
4. Below-average revenue
5. Unresolved/reopened support tickets

---

## Notebook Structure

| Section | Description |
|---|---|
| 0. Setup | Imports, settings, folder creation |
| 1. Data Loading | Load all 6 datasets, schema inspection |
| 2. Data Quality Audit | Missing values, duplicates, outliers, leakage |
| 3. Table Joins | Build Analytical Base Table (ABT) — 2400 x 27 |
| 4. EDA | 8 charts covering all business dimensions |
| 5. Churn-Risk Hypotheses | 5 evidence-backed hypotheses |
| 6. Summary | Key findings table |

---

## Notes

- `data/` folder is excluded from version control via `.gitignore`
- All orders after `2025-09-30` are excluded from features to prevent data leakage
- Post-snapshot orders exist in the raw data only for churn label construction
