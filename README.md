# Customer Segmentation & Retention Analysis

## Project Overview

This project analyzes customer purchasing behavior for a UK-based online gift retailer to answer a core business question:

**How can an online retailer identify high-value customers, detect churn risk early, and design targeted retention strategies using historical transaction data?**

Using transaction-level data, I built a full analytics pipeline covering data cleaning, customer feature engineering, behavioral segmentation, and cohort-based retention analysis. The result is an end-to-end customer analytics case study demonstrating how data-driven segmentation and retention insights can inform CRM and lifecycle marketing strategy.


## Dataset

**Source:** [UCI Online Retail II Dataset](https://archive.ics.uci.edu/dataset/502/online+retail+ii)  
**Time Range:** December 2009 – December 2011  
**Records:** ~780K cleaned transaction records  
**Entity:** UK-based online gift retailer

The dataset contains invoice-level purchase history including product quantities, prices, customer IDs, and timestamps.


## Phase 1 — Data Cleaning & Validation

**Goal:** Produce a clean transactional dataset suitable for customer-level behavioral analysis.

Key steps:
- Converted timestamps to proper datetime format  
- Removed transactions with missing customer IDs  
- Excluded canceled invoices and return records  
- Removed zero-price and negative-quantity transactions  
- Removed duplicate rows  
- Validated time coverage and schema consistency  

**Result:** A clean transaction table with valid purchase activity for downstream analysis.


## Phase 2 — Customer Segmentation

### Feature Engineering (SQL)

Built customer-level behavioral features including:

- Recency (days since last purchase)  
- Frequency (distinct order count)  
- Monetary value (total spend)  
- Average order value  
- Interpurchase gap  
- Active lifespan  
- Average items per order  
- Average unit price  

### Unsupervised Clustering Exploration

- Tested K-Means clustering on transformed and scaled features  
- Applied winsorization, log transformation, and RobustScaler  
- Evaluated cluster separation using elbow method, PCA visualization, and silhouette score  

**Finding:** Natural clusters were weak due to continuous behavioral gradients.  
**Decision:** Pivoted to business-driven RFM segmentation for interpretability and stability.

### RFM-Based Behavioral Segmentation

Customers were scored on:
- Recency  
- Frequency  
- Monetary value  

Then assigned into actionable segments:

- Champions  
- Loyal  
- Potential Loyalist  
- Promising  
- New Customers  
- Need Attention  
- About to Sleep  
- At Risk  
- Cannot Lose Them  
- Hibernating  

### Revenue Concentration Insight

- **Champions (~18% of customers) drive ~69% of total revenue**
- Loyal + Potential Loyalists represent high-growth opportunity segments

### Outcome

A fully interpretable customer segmentation framework aligned with business use-cases and marketing strategy design.


## Phase 3 — Retention & Cohort Analysis

### Cohort Construction

- Assigned each customer to a cohort based on first purchase month  
- Built customer-month activity table  
- Computed retention rates by months since cohort start  

### Retention Findings

- Sharp drop after first purchase indicates onboarding opportunity  
- Long-tail of repeat customers sustains revenue base  

### Segment-Level Retention

Joined RFM segments with cohort activity to compare long-term engagement:

- Champions and Loyal segments show strongest long-term retention  
- Hibernating and At Risk segments churn rapidly  

### Visualizations

- Overall retention curve  
- Segment-specific retention curves  
- Cohort heatmaps per segment  
- Weighted retention comparison across segments  


## Business Insights

- Retaining high-value repeat customers yields greater long-term revenue impact than focusing solely on acquisition  
- Early post-purchase onboarding is critical to reduce first-month churn  
- Targeted win-back campaigns for At Risk customers can recover lost value  
- Suppressing paid targeting for Hibernating customers reallocates budget to higher-return segments  


## Tech Stack

**SQL:** Microsoft SQL Server  
**Python:** Pandas, NumPy, Scikit-learn, Yellowbrick, Seaborn, Matplotlib, Plotly  
**Methods:** RFM segmentation, K-Means exploration, PCA, Cohort retention analysis  


## Key Takeaway

**Long-term revenue growth is more efficiently achieved by retaining and expanding high-value repeat customers than by focusing solely on new customer acquisition.**


## How to Run

```bash
python -m venv venv
source venv/bin/activate
pip install -r requirements.txt
```

Then run the SQL scripts in `/sql/` and the notebooks in `/notebooks/` in order.