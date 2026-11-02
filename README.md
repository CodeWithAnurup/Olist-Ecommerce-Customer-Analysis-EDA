# Olist E-commerce Customer Analysis (EDA)

> **Exploratory Data Analysis of 99,441 Brazilian e-commerce customer records to diagnose geographic distribution, urban market concentration, and repeat-purchase retention dynamics.**

---

## 📊 Project Overview

In fast-growing e-commerce marketplaces, top-line order volumes often hide structural retention bottlenecks. This project performs an in-depth exploratory data analysis on the **Olist Brazilian E-Commerce Customers Dataset**, analyzing **99,441 transaction records across 27 federal states and 4,119 municipalities**.

The core objective is to evaluate how customers are distributed geographically, how order frequency behaves across the user base, and where the marketplace faces operational concentration risks versus growth opportunities.

---

## 📖 The Data Story: The 3.1% Retention Bottleneck

When a startup tracks high-level vanity metrics, 99,441 total orders across multiple marketplaces looks like a healthy growth curve. However, unpacking the relationship between customer identifiers reveals a crucial marketplace reality:

```
Total Order Records:        99,441
Unique Human Customers:     96,096
Repeat Customers (≥ 2 orders): 3,345 (~3.1%)
One-Time Buyers:            92,751 (~96.9%)
```

### The "Leaky Bucket" Challenge
- **96.9% of all customers bought exactly once** and never returned to the platform.
- The repeat purchase rate is approximately **3.1%**.
- While a few extreme outliers exist—one power buyer placed **17 orders**, another placed **9 orders**, and a handful placed **7 orders**—the vast majority never generated ongoing lifetime value (LTV).
- **The Core Startup Takeaway:** If a business relies almost entirely on first-time buyers, customer acquisition cost (CAC) continuously burns cash reserves unless post-purchase retention loops are actively engineered.

---

## 🔍 Key Findings from the Dataset

### 1. Data Schema & ID Architecture
Olist utilizes a dual-identifier schema that separates transaction-level tokens from customer entities:
- **`customer_id` (renamed `customer_order_id` in pipeline):** Generated uniquely for every single order. It tracks the order-customer transaction pairing (99,441 distinct values, 0 duplicates, 0 nulls).
- **`customer_unique_id`:** Represents the actual distinct human buyer across their lifecycle (96,096 unique individuals).

### 2. Severe Geographic Concentration
Order demand is heavily skewed toward Brazil's southeastern economic center:
- **São Paulo (SP) Dominance:** State of São Paulo commands the largest share of order volume by a massive margin over all other 26 states.
- **Urban Concentration:**
  - **São Paulo City** accounts for **~15.6%** of all customers nationwide.
  - **São Paulo and Rio de Janeiro combined** account for **~22%** of total platform volume.
  - The **Top 15 cities represent ~39%** of the entire customer base.
  - **7 of the top 15 cities** are located inside São Paulo state (heavily concentrated within the Greater São Paulo metropolitan area).
  - The single most active customer (17 orders) is located in **São Paulo**.

### 3. Uniformly Flat Retention Across States
A crucial discovery from grouping repeat rates across all 27 states:
- Repeat purchase rates hover consistently at **~3% across every state**, regardless of whether it is an economic hub (SP, RJ, MG) or a remote territory (AC, RR, AP).
- **Diagnostic:** Low retention is **not a localized regional defect**; it is a **systemic, platform-wide challenge**.

---

## 💡 Startup Business Insights

| Dimension | Strategic Finding | Impact / Actionable Recommendation |
| :--- | :--- | :--- |
| **Concentration Risk** | 22% of customer volume is locked in just two urban metros (SP & RJ). | High operational sensitivity. Any regional delivery bottleneck, courier strike, or warehouse issue in SP/RJ threatens company-wide cash flow. |
| **Long-Tail Opportunity** | Over 4,000 smaller cities make up the remaining customer base. | While massive in aggregate, individual cities are highly fragmented. Localized marketing is cost-prohibitive without regional fulfillment partnerships. |
| **LTV / CAC Trap** | ~97% one-time buyer rate indicates high reliance on new user acquisition. | Transition focus from pure top-of-funnel ad spend to post-delivery re-engagement (email automation, loyalty incentives, replenishment offers). |

---

## ⚠️ Analytical Limitations & Boundaries

- **Single-Table Scope:** This analysis is conducted exclusively on `olist_customers_dataset.csv`. Because this table contains geographic and customer keys but no timestamps or revenue amounts, financial metrics (e.g., GMV, AOV) cannot be calculated directly here.
- **RFM Analysis Boundary:** A comprehensive Recency, Frequency, Monetary (RFM) model cannot be executed on customer demographics alone. Only the **Frequency** component is present in this dataset.

---

## 🚀 Future Scope & Engineering Roadmap

1. **Orders Table Integration:** Join with `olist_orders_dataset.csv` to calculate actual delivery lead times and test the hypothesis that shipping delays drive one-time drop-offs.
2. **Review Score Correlation:** Merge `olist_order_reviews_dataset.csv` to correlate 1-star customer ratings with churn probability.
3. **Zip-Code Geolocation Modeling:** Utilize the geolocation table to calculate geographic distance between sellers and buyers to evaluate delivery radius friction.
4. **Post-Delivery Verification:** Automate delivery verification and customer feedback loops to diagnose return friction and product mismatch early.

---

## 🛠️ Tech Stack & Dependencies

- **Language:** Python 3.10+
- **Data Manipulation:** `pandas`, `numpy`
- **Data Visualization & Profiling:** `seaborn`, `matplotlib`, `ydata-profiling`
- **Interactive Report:** `olist_report.html` (Automated HTML profiling report)
- **Environment:** Jupyter Notebook (`Notebook_EDA.ipynb`)

---

## 💻 How to Run the Analysis

1. **Clone the repository:**
   ```bash
   git clone https://github.com/CodeWithAnurup/Olist-Ecommerce-Customer-Analysis-EDA.git
   cd Olist-Ecommerce-Customer-Analysis-EDA
   ```

2. **Install required packages:**
   ```bash
   pip install pandas numpy seaborn matplotlib ydata-profiling
   ```

3. **Launch the notebook:**
   ```bash
   jupyter notebook Notebook_EDA.ipynb
   ```
