# 🍔 QuickBite Express: Crisis Impact & Recovery Analysis

**An interactive Power BI dashboard analyzing the June–September 2025 crisis of a Bengaluru-based food delivery startup, and recommending how the business can recover.**

> **Note on numbers:** Values marked **NA** are not available in my dashboard. Values marked with **~** are derived from the dashboard's monthly figures (simple averages of the monthly values shown), not read directly from a single card.

---

## 📋 Table of Contents

1. [Project Overview](#-project-overview)
2. [Problem Statement](#-problem-statement)
3. [Dataset Description](#-dataset-description)
4. [Methodology](#-methodology)
5. [Key Findings](#-key-findings)
6. [Recommendations](#-recommendations)
7. [Technical Implementation](#-technical-implementation)
8. [Deliverables](#-deliverables)
9. [Sources & References](#-sources--references)
10. [How to Explore](#-how-to-explore)

---

## 🎯 Project Overview

**Project Type:** Business Case Analysis | Data Analytics
**Domain:** Food Delivery & Consumer Analytics
**Time Period Analyzed:** January – September 2025
**Focus:** Crisis Analysis & Recovery Strategy Development
**Tools Used:** Power BI, DAX
**Audience:** Data Analysts, Business Strategists, Recruiters

### Executive Summary

In June 2025, QuickBite Express, a Bengaluru-based food delivery startup (founded 2020), faced a critical crisis triggered by:

- A viral food safety incident involving partner restaurants
- A week-long delivery outage during the monsoon season
- Aggressive competitor campaigns capitalizing on the operational failures

**Crisis Impact (from the dashboard):**

- Orders fell from **52.4K** (Jan–May) to **25.3K** (Jun–Sep), a **51.7% decline** in total orders.
- Monthly revenue dropped from about **3.3M–3.6M** to about **2M**.
- Average customer rating fell from about **4.3 to about 3.0**.
- SLA compliance collapsed from **44% to 12%**.
- Average delivery time rose from **39 to 60 minutes**.
- Cancellation rate roughly doubled, from about **6% to about 12%**.
- Customers churned: **NA**
- Restaurant partner exodus: **NA**

**Key Discovery:** The damage was not uniform. **Kolkata (42.9%)** and **Hyderabad (38.9%)** lost the most orders, while **Bengaluru** had the highest crisis cancellation rate (**15.2%**). Negative reviews were dominated by food quality, food safety and packaging complaints.

**Strategic Output:** Three data-backed recovery priorities (delivery reliability and SLA in high-impact cities, food safety monitoring, and customer win-back campaigns). Total investment, expected recovery and ROI: **NA**.

---

## 💼 Problem Statement

### Business Challenge

QuickBite Express needs a comprehensive analysis of its June–September 2025 crisis to:

1. **Understand Crisis Severity:** Quantify impact across all business metrics
2. **Identify Root Causes:** Determine what triggered the cascade of failures
3. **Customer Impact Analysis:** Segment churned customers by recovery probability
4. **Competitive Context:** Benchmark against industry peers during the crisis
5. **Recovery Strategy:** Design a data-backed turnaround plan with timelines and ROI
6. **Operational Insights:** Identify systemic vulnerabilities to prevent recurrence

### Analysis Questions Addressed

**Primary Analysis (10 questions):**

| # | Question | Status in this dashboard | Result |
|---|---|---|---|
| 1 | Monthly order decline comparison (pre-crisis vs crisis) | ✅ Covered | 52.4K → 25.3K (-51.7%) |
| 2 | Top 5 cities by order decline percentage | ✅ Covered | Kolkata 42.9%, Hyderabad 38.9%, Pune 9.1%, Bengaluru 5.7%, Mumbai -13.3% (growth) |
| 3 | Top 10 high-volume restaurants with largest decline | NA | NA |
| 4 | Cancellation rate trend analysis and geographic impact | ✅ Covered | ~5.9% → ~11.9%; Bengaluru highest at 15.2% |
| 5 | Delivery SLA performance degradation | ✅ Covered | 44% → 12% |
| 6 | Monthly customer rating fluctuations | ✅ Covered | ~4.30 → ~3.07 |
| 7 | Negative keyword sentiment analysis | ✅ Covered | Top review themes ranked by count |
| 8 | Revenue impact quantification | ✅ Covered | ~3.49M → ~1.97M average per month |
| 9 | Loyalty impact on 5+ order customers with 4.5+ ratings | NA | NA |
| 10 | High-value customer (top 5%) decline patterns | NA | NA |

**Secondary Analysis:**

| Question | Status | Result |
|---|---|---|
| Competitor comparison (Swiggy, Zomato performance) | NA | NA |
| External factors contributing to CAC tripling | NA | NA |
| Most effective recovery strategies | Partially covered | Three recommended priorities (see Recommendations) |
| Restaurant type churn risk assessment | NA | NA |
| Lapsed customer return probability | NA | NA |
| Priority cities risk analysis | ✅ Covered | Map of cities at highest risk of demand loss |
| Customer order value shift behavior | NA | NA |
| Review spike correlation with delivery outage | NA | NA |

---

## 📊 Dataset Description

### Data Sources

| Data Type | Source | Time Period | Records | Key Metrics |
|---|---|---|---|---|
| Orders | Codebasics challenge dataset | Jan–Sep 2025 | ~77.7K orders (52.4K pre-crisis + 25.3K crisis) | total orders, city, month, phase, revenue |
| Customers | Codebasics challenge dataset | Jan–Sep 2025 | NA | NA |
| Reviews & Ratings | Codebasics challenge dataset | Jan–Sep 2025 | NA | rating, review theme, month |
| Restaurant Data | Codebasics challenge dataset | Jan–Sep 2025 | NA | NA |
| Operational Metrics | Codebasics challenge dataset | Jan–Sep 2025 | NA | avg delivery time, SLA compliance, cancellations |

### Key Fields & Definitions

**Phase Classification:**

- **Pre-Crisis:** January – May 2025 (5 months baseline)
- **Crisis:** June – September 2025 (4 months of operational failure)

**Customer Segmentation:** Total customers: NA | Active (pre-crisis): NA | Active (crisis): NA | Churned: NA | New: NA | Retained: NA

**Order Metrics:**

- Pre-crisis total: **52.4K** (monthly average ~10.5K)
- Crisis total: **25.3K** (monthly average ~6.3K)
- Decline in total orders: **51.7%** (52.4K → 25.3K)
- Decline in monthly average orders: **~39.6%** (the two phases have different lengths, 5 vs 4 months)

**Revenue Metrics (currency not labelled in the dashboard):**

- Pre-crisis total: ~17.46M (5 months) | monthly average ~3.49M
- Crisis total: ~7.88M (4 months) | monthly average ~1.97M
- Decline in monthly average revenue: **~43.6%**

---

## 🔬 Methodology

### 1. Data Analysis Framework

#### A. Descriptive Analysis

**Purpose:** Understand the current state and crisis severity.

**Metrics Calculated:**

- Order volume by month and city
- Monthly revenue
- Customer counts by status (active, churned, new, retained): NA
- Cancellation rates and SLA compliance trends
- Average delivery time
- Average ratings and negative review themes

**Tools:** Power BI aggregations and DAX measures

#### B. Comparative Analysis

**Purpose:** Quantify pre-crisis vs crisis changes.

**Methodology:** Decline % = (Pre-Crisis Value − Crisis Value) / Pre-Crisis Value × 100

**Example, order decline:** (52.4K − 25.3K) / 52.4K × 100 = **51.7%**

**Applied to:** Orders, revenue, ratings, cancellations, SLA compliance, delivery time

#### C. Customer Segmentation

**Purpose:** Identify recoverable customers.

- High return probability segment: NA
- Medium return probability segment: NA
- Low return probability segment: NA

*Not part of this dashboard. Listed as future scope.*

#### D. Revenue Impact Analysis

**Purpose:** Quantify financial loss.

- Monthly revenue: **3.58M, 3.31M, 3.63M, 3.41M, 3.53M** (Jan–May) vs **2.03M, 1.96M, 1.94M, 1.95M** (Jun–Sep)
- Breakdown by subtotal, delivery fee and discounts: NA
- Total revenue lost: NA (the two phases have different lengths, so monthly averages are compared instead)

#### E. Sentiment Analysis

**Purpose:** Understand changes in customer perception.

**Method:** Review theme frequency analysis plus monthly average rating tracking.

| Pre-Crisis Avg Rating | Crisis Avg Rating | Change |
|---|---|---|
| ~4.30 | ~3.07 | -1.23 (-28.6%) |

**Top Negative Review Themes (crisis):**

| Theme | Reviews |
|---|---|
| Food quality issues | 1,109 |
| Food safety issues | 727 |
| Packaging issue | 711 |
| Bad taste | 693 |
| Not recommended | 693 |
| Stale food served | 686 |

Rating-based sentiment scoring: NA

### 2. Customer Acquisition Cost (CAC) Analysis

| Item | Value |
|---|---|
| Pre-crisis CAC | NA |
| Crisis CAC | NA |
| Increase | NA |
| Contributing factors (GST, ad costs, seasonality, brand damage) | NA |

### 3. Recovery Strategy ROI Modeling

| Pillar | Investment | Expected Impact | Timeline |
|---|---|---|---|
| Customer reactivation | NA | NA | NA |
| Food safety certifications | NA | NA | NA |
| Operational excellence | NA | NA | NA |
| Restaurant support | NA | NA | NA |
| **Total roadmap** | NA | NA | NA |

### 4. Competitive Benchmarking

| Competitor | Market Share | Revenue Growth | Strategy |
|---|---|---|---|
| Zomato | NA | NA | NA |
| Swiggy | NA | NA | NA |

Impact on QuickBite (app ranking, customers lost to competitors): NA

---

## 📈 Key Findings

### Crisis Impact Summary

| Metric | Pre-Crisis | Crisis | Change | % Change |
|---|---|---|---|---|
| Total Orders | 52.4K | 25.3K | -27.1K | -51.7% |
| Avg Monthly Orders | ~10.5K | ~6.3K | ~-4.2K | ~-39.6% |
| Avg Monthly Revenue | ~3.49M | ~1.97M | ~-1.52M | ~-43.6% |
| Total Revenue (period) | ~17.46M | ~7.88M | ~-9.58M | ~-54.9% |
| Active Customers | NA | NA | NA | NA |
| Avg Rating | ~4.30 | ~3.07 | -1.23 | -28.6% |
| SLA Compliance | 44% | 12% | -32 pts | -72.7% |
| Avg Delivery Time | 39 min | 60 min | +21 min | +53.8% |
| Cancellation Rate | ~5.9% | ~11.9% | +6.0 pts | ~+101% |

> Total orders and total revenue compare a 5-month period with a 4-month period. The monthly average rows give a like-for-like comparison.

### City-Level Findings

| City | Order Decline % | Crisis Cancellation Rate |
|---|---|---|
| Kolkata | 42.9% | NA |
| Hyderabad | 38.9% | 9.1% |
| Pune | 9.1% | NA |
| Bengaluru | 5.7% | 15.2% |
| Mumbai | -13.3% (orders grew) | NA |
| Chennai | NA | 9.1% |
| Delhi | NA | 6.7% |

### Root Causes

**Primary (Operational):**

1. SLA compliance collapsed from 44% to 12%
2. Average delivery time jumped from 39 to 60 minutes
3. Cancellations roughly doubled, with Bengaluru the worst at 15.2%

**Secondary (Reputational):**

1. Viral food safety incident (from the case background)
2. Average rating fell from ~4.30 to ~3.07
3. Top complaints: Food quality (1,109), Food safety (727), Packaging (711)
4. Share of negative reviews by September: NA

**Tertiary (Competitive):**

1. Competitors ran aggressive campaigns during the crisis (from the case background)
2. Share of lost customers captured by competitors: NA

**External (Market):**

1. Monsoon-season delivery outage (from the case background)
2. GST impact, ad cost increases, seasonality impact: NA

### Recovery Opportunity

**Recoverable Customer Base:**

- High-priority customers: NA
- Revenue at risk: NA
- Geographic concentration: highest order decline in **Kolkata (42.9%)** and **Hyderabad (38.9%)**; highest cancellations in **Bengaluru (15.2%)**
- Cities at highest risk of demand loss (map): Delhi, Ahmedabad, Mumbai, Pune, Hyderabad, Bengaluru, Chennai, Kolkata
- Order frequency recovery potential: NA

**Key Insight:** The crisis was driven by operational failures (slow deliveries, cancellations) and trust problems (food quality and safety), and some cities were hit far harder than others. That makes it addressable through targeted operational fixes and win-back efforts in specific markets.

---

## 💡 Recommendations

| # | Recommendation | Target | Dashboard Evidence | Expected Impact | Investment | Timeline |
|---|---|---|---|---|---|---|
| 1 | **Improve delivery reliability and SLA performance in high-impact cities** | Kolkata, Hyderabad, Bengaluru | SLA 44% → 12%; delivery time 39 → 60 min; Bengaluru cancellations 15.2% | NA | NA | NA |
| 2 | **Strengthen food safety monitoring across partner restaurants** | All partner restaurants | Top complaints: food quality (1,109), safety (727), packaging (711), stale food (686) | NA | NA | NA |
| 3 | **Run targeted campaigns to win back previously loyal customers** | Lapsed customers in high-risk cities | Orders -51.7%; rating ~4.30 → ~3.07 | NA | NA | NA |

**Total Recovery Roadmap:** Total investment: NA | Timeline: NA | Expected recovery: NA | Cumulative ROI: NA

---

## 🛠️ Technical Implementation

### Tools & Technologies Used

**Data Visualization:**

- **Power BI Desktop:** Interactive dashboard, **2 pages**
- **Visual Types:** KPI cards, line charts, column charts, horizontal bar chart, table, map, slicer
- **DAX Functions:** NA

**Data Analysis:**

- **DAX Measures:** Order Decline %, Pre-Crisis and Crisis Orders, Cancellation Rate % (pre-crisis and crisis), Average Delivery Time, SLA Compliance %. Total number of custom measures: NA
- **Calculations:** Pre/post-crisis comparisons, trend analysis, review theme counts
- **Modeling:** Customer lifetime value, churn probability, recovery potential: NA

### Methodology References

**Statistical Analysis:**

- **Churn Modeling:** NA
- **Risk Scoring:** NA
- **ROI Calculation:** NA
- **Probability Assessment:** NA

**Data Analysis Best Practices:**

- **Comparative Analysis:** Pre/post-crisis methodology
- **Customer Segmentation:** NA
- **Sentiment Analysis:** Review theme frequency analysis with rating trends
- **Benchmark Validation:** NA

---

## 📦 Deliverables

| Deliverable | Status |
|---|---|
| Power BI dashboard (.pbix), 2 pages | ✅ |
| Dashboard screenshots | ✅ |
| README documentation | ✅ |
| Presentation / video walkthrough | NA |

---

## 📚 Sources & References

- **Data and case study:** Codebasics Data Analytics Project Challenge (simulated dataset for a fictional company). Link: `[add the challenge URL here]`
- **Competitor and market research:** NA
- **External industry reports:** NA

---

## 🔍 How to Explore

**For Orders and Operational Insights:**

- **Page 1 (Performance Analysis):** Orders, cancellation trend, delivery time, SLA compliance
- Root cause of cancellations by city

**For Customer and Revenue Insights:**

- **Page 2 (Customer Experience & Revenue Impact):** Revenue by month, ratings, negative review themes
- Use the **Period slicer** (Crisis / Pre-Crisis) to filter the report

**For Strategic Understanding:**

- Cities at highest risk of demand loss (map on Page 2)
- Top 5 cities by order decline (table on Page 1)
- Recovery recommendations in this README

---

## 🖼️ Dashboard Preview

**Page 1: Performance Analysis**

![Dashboard Page 1](images/dashboard_page1.png)

**Page 2: Customer Experience & Revenue Impact**

![Dashboard Page 2](images/dashboard_page2.png)

---

## 🙋 About Me

**[Your Name]**
Data Analyst | Power BI · SQL · Python · Excel
🔗 [LinkedIn](https://linkedin.com/in/your-profile) · 📧 your.email@example.com
