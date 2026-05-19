# Business Memo

**To:** Product, Marketing & Customer Success Teams  
**From:** Data Analytics  
**Date:** 2025-09-30  
**Subject:** Key Customer Behaviour Patterns to Investigate Before Launching Retention Campaign

---

## Executive Summary

An analysis of 2,400 customers reveals a **47% churn rate** in the 60-day window following September 2025. This is significantly high and requires targeted, data-backed intervention rather than blanket discounting. The following findings should guide the retention strategy.

---

## Key Findings

### 1. Purchase Frequency is the Strongest Churn Signal

Churned customers placed an average of **3.04 orders** compared to **3.70 orders** for retained customers. Customers with declining order frequency should be flagged early — before they go completely silent.

**Recommended action:** Build an early-warning trigger for customers whose order frequency drops below 3 orders in the observation window.

---

### 2. Revenue Gap Between Churned and Retained Customers

Retained customers generated an average revenue of **₹2,839** vs **₹2,222** for churned customers — a **22% revenue gap**. This confirms that churned customers were already lower-value before churning.

**Recommended action:** Prioritise retention spend on mid-to-high revenue customers showing early churn signals, not low-revenue customers who may not be worth the retention cost.

---

### 3. App Engagement Drops Sharply Before Churn

Churned customers averaged only **4.02 sessions** in the last 30 days vs **6.73 sessions** for retained customers. More critically, churned customers had not visited the app for an average of **26.55 days** before the snapshot, compared to just **9.77 days** for retained customers.

**Recommended action:** Trigger automated re-engagement notifications for customers inactive for 14+ days. This is an early and actionable signal.

---

### 4. Support Ticket Issues Are Evenly Distributed — Volume Matters More Than Type

Issue type distribution is nearly identical between churned and retained customers across all categories (late_delivery, damaged_item, refund_delay etc.). However, churned customers have slightly higher resolution times (**24.35 hrs** vs **24.66 hrs**).

**Recommended action:** Focus on reducing resolution time overall. Customers with reopened tickets (`reopened=1`) should be escalated immediately as they signal unresolved dissatisfaction.

---

### 5. Return Behaviour is Comparable — Not a Primary Driver

Average returns are nearly identical (0.23 for retained vs 0.22 for churned). Returns alone do not predict churn, but combined with low session count and low order frequency, they form a high-risk profile.

**Recommended action:** Do not use return rate in isolation. Use it as one signal in a combined risk score.

---

## What the Company Should Investigate Before Launching Any Retention Campaign

1. **Segment customers by combined risk score** — low orders + low sessions + high last_visit_days — rather than targeting all churners with the same offer.

2. **Investigate the 1,153 customers with zero support tickets** — these silent customers may be disengaged without ever complaining, making them hard to detect but important to retain.

3. **Audit campaign effectiveness** — the intervention_history data shows prior campaigns were sent. Analyse whether customers who received campaigns churned at a lower rate before spending on new campaigns.

4. **Do not offer blanket discounts** — the data shows churned customers were already lower revenue. Discounting them further reduces margin without guarantee of retention.

5. **Focus on the 18-24 and 25-34 age segments** — EDA shows these groups have the highest representation and merit segment-specific messaging.

---

## Conclusion

The data points to **low engagement and low purchase frequency** as the most actionable early churn signals. The company should prioritise building a behavioural trigger system over broad-based discount campaigns. A targeted approach based on session activity and order recency will yield better ROI on retention spend.
