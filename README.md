# Telco Customer Church Analysis Project
### End-to-End Case Study

**Dataset:** IBM Telco Customer Churn (7,043 customers × 21 features)  
**Goal:** Understand what drives churn, build a predictive model, and generate actionable retention strategies

### Table of Contents
1. [Problem Framing](#1-problem-framing)
2. [Data Loading & Cleaning](#2-data-loading--cleaning)
3. [Exploratory Data Analysis](#3-exploratory-data-analysis)
4. [Feature Engineering](#4-feature-engineering)
5. [Churn Modelling](#5-churn-modelling)
6. [Model Evaluation](#6-model-evaluation)
7. [Postdictive Analysis](#7-postdictive-analysis)
8. [Business Recommendations](#8-business-recommendations)


## 1. Problem Framing

### What is churn in this business context?

**Customer churn** refers to the event where a subscriber voluntarily terminates their relationship with a telecommunications provider — discontinuing their phone, internet, or bundled service contract. In this dataset, churn is a binary outcome (`Yes`/`No`) recorded at a point in time for each customer.

This is a **supervised binary classification** problem: given a customer's historical service, usage, and billing attributes, predict whether they will churn.

---

### Why does churn matter?

| Metric | Typical industry figure |
|--------|------------------------|
| Cost to acquire a new customer | 5–7× the cost to retain one |
| Revenue at risk (26.5% churn) | ~$1 in every $4 of recurring revenue |
| Payback on retention campaigns | 3–10× ROI when targeted correctly |

Reducing churn by even **5 percentage points** can increase profitability by **25–95%** (Harvard Business Review). Churn analysis sits at the intersection of data science and revenue protection — it is one of the highest-impact analytics use cases in any subscription business.

---

### Analytical approach

```
Data → Clean → EDA → Feature Engineering → Model → Evaluate → Interpret → Recommend
```

Three models are benchmarked:
- **Logistic Regression** — interpretable linear baseline
- **Random Forest** — ensemble, handles non-linearity well
- **Gradient Boosting** — strong performer, used for SHAP interpretation

Primary metric: **ROC-AUC** (handles class imbalance well). Secondary: Precision-Recall (AP).

---
## 2. Data Loading & Cleaning
### Dataset Overview

| Attribute | Detail |
|--------|------------------------|
| Rows | Rows	7,043 customers |
| Columns | 21 (20 features + 1 target) |
| Target | Target	Churn (Yes / No) |
| Numeric features | Numeric features	tenure, MonthlyCharges, TotalCharges |
| Categorical features | 17 (gender, contract, internet service, etc.) |
| Missing values (raw) | 11 blank TotalCharges entries |

### Cleaning Decisions
-	TotalCharges stored as a string object — converted to float64.
-	11 blank TotalCharges entries correspond to customers with tenure = 0 (brand-new accounts with no billing history). Filled with 0.0 — the correct business interpretation.
-	No duplicate records found.
-	Churn re-encoded as Churn_bin (0/1) for modelling.
-	All 11 "missing" values resolved; final dataset is 100% complete.
