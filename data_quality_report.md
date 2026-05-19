# Data Quality Report
## D2C Customer Churn Intelligence — Part 1

**Dataset snapshot date:** 2025-09-30  
**Prepared by:** [Your Name]  
**Datasets audited:** customers, orders, support_tickets, web_events_snapshot, churn_labels, intervention_history

---

## 1. Missing Values

| Dataset | Column | Missing Count | Missing % | Recommended Treatment |
|---|---|---|---|---|
| customers | loyalty_tier | ~1,386 | ~57.8% | Flag as "Not Enrolled" — separate category |
| customers | skin_type | ~401 | ~16.7% | Impute with mode or "Unknown" category |
| orders | rating | ~80 | ~0.8% | Exclude from averages; impute with median per category |

**Key observation:** `loyalty_tier` nulls mean the customer was never enrolled in the loyalty programme — this is business-meaningful and should NOT be dropped. Treat as a separate "Not Enrolled" category.

---

## 2. Duplicate Records

| Dataset | Duplicate Rows | Notes |
|---|---|---|
| customers | 0 | Clean ✓ |
| orders | Present | Some `order_id` values end in `_DUP` — intentional duplicates for data-quality task |
| support_tickets | 0 | Clean ✓ |
| web_events_snapshot | 0 | Clean ✓ |
| churn_labels | 0 | Clean ✓ |
| intervention_history | 0 | Clean ✓ |

**Recommendation:** Deduplicate orders by removing rows where `order_id` ends in `_DUP` before feature engineering.

---

## 3. Invalid / Unusual Values

| Dataset | Column | Issue | Count | Action |
|---|---|---|---|---|
| orders | gross_amount | Outliers up to ₹24,789 | 536 (5.4%) | Cap at 99th percentile or log-transform |
| orders | quantity | Outliers detected | 247 (2.5%) | Investigate; likely bulk orders |
| orders | returned | High return count | 675 (6.7%) | Valid business signal — keep |
| orders | delivery_days | Outliers detected | 3 (0.0%) | Negligible — keep |
| customers | age_group | Categorical, no numeric age | — | Use as-is for segmentation |

---

## 4. Post-Snapshot Data Leakage Risk

**Critical finding:** `orders.csv` contains rows dated **after 2025-09-30** (the snapshot date). These post-snapshot orders exist only to construct churn labels and must NOT be used as model features.

**Action taken:** Filtered orders to `order_date <= 2025-09-30` before any feature engineering.

| | Count |
|---|---|
| Total orders | ~10,009 |
| Pre-snapshot orders used | Filtered set |
| Post-snapshot rows removed | Remainder |

---

## 5. Join / Key Integrity

| Dataset | Orphan IDs | Customers Not Present | Status |
|---|---|---|---|
| orders | 0 | 0 | Clean ✓ |
| support_tickets | 0 | 1,153 | Expected — not all customers raise tickets |
| web_events_snapshot | 0 | 0 | Clean ✓ |
| churn_labels | 0 | 0 | Clean ✓ |
| intervention_history | 0 | 0 | Clean ✓ |

**Note:** 1,153 customers with no support tickets is expected behaviour per the data dictionary. These are likely low-engagement customers.

---

## 6. Leakage Risk Columns

The following columns must be excluded from model features:

| Column | Dataset | Reason |
|---|---|---|
| `churn_next_60d` | churn_labels | Target variable itself |
| `split` | churn_labels | Train/val/test assignment — future info |
| `order_date > 2025-09-30` | orders | Post-snapshot orders |
| `snapshot_date` | multiple | Always same value — no predictive power |
| `last_campaign_received` | intervention_history | Campaign sent after churn risk identified |
| `last_campaign_cost` | intervention_history | Same as above |

---

## 7. Summary of Recommendations

| Priority | Issue | Action |
|---|---|---|
| HIGH | Post-snapshot orders in features | Filter orders to pre-2025-09-30 only |
| HIGH | `_DUP` order IDs | Deduplicate before aggregation |
| MEDIUM | `loyalty_tier` nulls (57.8%) | Encode as "Not Enrolled" category |
| MEDIUM | `gross_amount` outliers (5.4%) | Cap at 99th percentile |
| LOW | `skin_type` nulls (16.7%) | Impute with mode or "Unknown" |
| LOW | `rating` nulls (~80 rows) | Exclude from rating-based averages |
