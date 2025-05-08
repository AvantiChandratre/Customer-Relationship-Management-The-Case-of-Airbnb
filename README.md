# Airbnb Host Retention Optimization

**Maximizing net profit by selectively gifting at-risk hosts**

---


## Project Overview

Airbnb sought to reduce host churn by offering a \$1,000 retention gift to those most likely to de-list. In this project we:

* Built a churn-prediction model
* Designed a gift-allocation mechanism to maximize net commission revenue
* Benchmarked business outcomes **with** and **without** targeted gifting

## Business Problem & Impact

* **Problem:** Host churn shrinks Airbnb’s supply and future earnings.
* **Opportunity:** A \$1,000 gift can retain key hosts and recoup more than its cost via Airbnb’s 15% commission.
* **Impact:** Strategic gifting yields positive ROI and stabilizes host inventory.

## Approach & Methodology

1. **Feature Engineering**

   * Aggregated reservation patterns, host vintage (`nmon`), ratings, bedrooms/bathrooms
   * Created geographic clusters via K-Means on latitude/longitude
   * One-hot encoded categorical features

2. **Model Training & Selection**

   * Evaluated multiple classifiers: Logistic Regression, Decision Tree, Random Forest, GBT
   * **Final Model:** Random Forest (`max_depth=8`, `max_features=0.5`, `max_samples=0.7`, `n_estimators=500`)
   * **Validation ROC-AUC:** **0.81**

## Data Sources

* **Host Data:** Monthly nights booked, revenue history
* **Host Attributes:** Ratings, number of listings, vintage
* **Geolocation:** Latitude & longitude for cluster assignment

## Modeling & Performance

| Model                 | ROC‑AUC  |
| --------------------- | -------- |
| Logistic Regression   | 0.72     |
| Decision Tree         | 0.75     |
| **Random Forest**     | **0.81** |
| Gradient Boosted Tree | 0.80     |

## Gift Allocation Logic

* **Assumptions:**

  * Airbnb commission = 15% of host revenue
  * All gifted hosts are retained
  * Host revenue remains at last year’s level

* **Net Benefit per Host:**

```
Commission = 0.15 × HostRevenue
GiftCost = 1,000
NetGain = Commission - GiftCost
```

* **Selection Rule:**

  1. Predict churn probability for each host.
  2. Filter for hosts with `NetGain > 0` (i.e., revenue > \$6,667).
  3. Rank by predicted churn risk and NetGain.
  4. Gift to top N hosts to maximize total NetGain.

## Scenario Comparison

| Scenario           | Commission Recovered                 | Gift Cost                 | Net Profit            |
| ------------------ | ------------------------------------ | ------------------------- | --------------------- |
| No Gift (Baseline) | \$0                                  | \$0                       | \$0                   |
| Model-Driven Gift  | Σ(0.15 × Revenue) for selected hosts | 1,000 × (Number of gifts) | Commission – GiftCost |

## Results & Key Findings

* **Threshold Identified:** Hosts with annual revenue > \$6,667

* **Optimal Gift Pool:** Top 150 at-risk, high-revenue hosts

* **Outcome:**

  * **Total Commission Recovered:** \$X
  * **Total Gift Cost:** \$Y
  * **Net Profit:** \$Z (an X% uplift vs. baseline)

## Conclusion & Award

This targeted gifting strategy delivers significant net profit and supply stability.

🏆 **First Place in Class** for its rigorous “no-gift vs. gift” comparison and clear business impact.

---

## How to Run

```bash
git clone https://github.com/your-org/airbnb-host-retention.git
cd airbnb-host-retention
pip install -r requirements.txt
jupyter lab
```

## Team

* Avanti
* Prashast
* Soutik
