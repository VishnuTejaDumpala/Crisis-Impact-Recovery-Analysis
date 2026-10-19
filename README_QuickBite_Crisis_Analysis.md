# QuickBite Express - Crisis Impact & Recovery Analysis

In June 2025, QuickBite Express saw its monthly orders collapse from ~23K to ~9K and lost 73K of its 105K customers in just four months.
This repository contains my complete Power BI analysis of what went wrong, and how data can guide the recovery.

**A data-driven analysis of a food delivery startup's crisis and the evidence behind its recovery strategy.**

> **Note on numbers:** Every figure below comes from my Power BI dashboard, which is built on the Codebasics challenge dataset. Where this project did not analyse something (competitors, CAC, investment and ROI), the value is marked **NA**. Values marked **~** are rounded or derived from the dashboard's monthly figures.

---

## 📋 Table of Contents

1. Project Overview
2. Problem Statement
3. Dataset Description
4. Methodology
5. Key Findings
6. Recommendations
7. Technical Implementation
8. Deliverables
9. Sources & References
10. How to Explore

---

## 🎯 Project Overview

**Project Type:** Business Case Analysis | Data Analytics  
**Domain:** Food Delivery & Consumer Analytics  
**Time Period Analyzed:** January - September 2025  
**Focus:** Crisis Analysis & Recovery Strategy Development  
**Tools Used:** Power BI, DAX  
**Audience:** Data Analysts, Business Strategists, Recruiters

### Executive Summary

In June 2025, QuickBite Express - a Bengaluru-based food delivery startup (founded 2020) - faced a critical crisis triggered by:
- A viral food safety incident involving partner restaurants
- A week-long delivery outage during the monsoon season
- Aggressive competitor campaigns capitalizing on the operational failures

**Crisis Impact:**
- 73K customers churned (73% of the 100K active base, 69% of all 105K customers)
- ₹2.7 Cr (₹26.7M) revenue lost: ₹3.76 Cr in the 5 pre-crisis months vs ₹1.09 Cr in the 4 crisis months
- Customer ratings collapsed from 4.5 → 2.5 stars (2.3 by September)
- Partner retention rate of 0.79: 21% of restaurants were not active in both periods, and active restaurants per month roughly halved (13.1K → 6.5K)

**Key Discovery:**
The decline was **uniform across every city (68-70%) and every cuisine (68.5-70.3%)**, while SLA compliance fell from 44% to 12% and delivery delays grew 8.7×. This points to a platform-wide service and trust failure, not a shift in customer preferences.

**Strategic Output:**
Three data-backed recovery priorities (delivery reliability, food safety monitoring, targeted win-back) and a city-level **recovery potential of ~₹8.5M** (about 32% of the lost revenue), concentrated in Bengaluru, Delhi and Mumbai. Investment, timeline and ROI: **NA**.

---

## 💼 Problem Statement

### Business Challenge

QuickBite Express requires a comprehensive analysis of its June-September 2025 crisis to:

1. **Understand Crisis Severity:** Quantify impact across all business metrics
2. **Identify Root Causes:** Determine what triggered the cascade of failures
3. **Customer Impact Analysis:** Segment churned customers by recovery probability
4. **Competitive Context:** Benchmark against industry peers during the crisis
5. **Recovery Strategy:** Design a data-backed turnaround plan
6. **Operational Insights:** Identify systemic vulnerabilities to prevent recurrence

### Analysis Questions Addressed

**Primary Analysis (10 questions):**
1. Monthly order decline comparison (pre-crisis vs crisis) - *Page 2*
2. Top 5 cities by order decline percentage - *Page 2*
3. Top 10 high-volume restaurants with largest decline - *Page 6 (grouped by restaurant name)*
4. Cancellation rate trend analysis and geographic impact - *Pages 2 and 5*
5. Delivery SLA performance degradation - *Page 5*
6. Monthly customer rating fluctuations - *Page 7*
7. Negative keyword sentiment analysis - *Page 7*
8. Revenue impact quantification - *Page 2*
9. Loyalty impact on 5+ order customers with 4.5+ ratings - *Page 3*
10. High-value customer (top 5%) decline patterns - *Page 4*

**Secondary Analysis (5 questions + 3 extra details):**
- Competitor comparison (Swiggy, Zomato performance) - **NA** (not covered)
- External factors contributing to CAC tripling - **NA** (not covered)
- Most effective recovery strategies - *Recovery potential model, Page 8*
- Restaurant type churn risk assessment - *Pages 6 and 8 (cloud kitchen vs restaurant, restaurant size, risk level)*
- Lapsed customer return probability - *Return segments, Page 8*
- Priority cities risk analysis - *City tiers, Page 8*
- Customer order value shift behavior - *Price tiers, Page 8*
- Review spike correlation with delivery outage - *SLA delay vs % negative reviews, Page 8*

---

## 📊 Dataset Description

### Data Sources

The dataset is the simulated QuickBite Express data from the **Codebasics Resume Project Challenge**, loaded as 8 tables in a star-schema model.

| Data Type | Table(s) | Time Period | Records | Key Fields |
|-----------|----------|-------------|---------|------------|
| **Orders** | fact_orders | Jan-Sep 2025 | 149K orders (149,166) | order_id, customer_id, restaurant_id, order_timestamp, subtotal_amount, discount_amount, delivery_fee, total_amount, is_cancelled |
| **Customers** | dim_customer | Jan-Sep 2025 | 105K customers with orders (107,776 in table) | customer_id, signup_date, city, acquisition_channel |
| **Reviews & Ratings** | fact_ratings | Jan-Sep 2025 | 69K reviews (68,825 after removing blank rows) | rating, sentiment_score, review_text, review_timestamp |
| **Restaurant Data** | dim_restaurant | Jan-Sep 2025 | 20K restaurants (19,995) | restaurant_id, restaurant_name, city, cuisine_type, partner_type |
| **Delivery Partners** | dim_delivery_partner | Jan-Sep 2025 | 15K partners | delivery_partner_id, vehicle_type, city, employment_type |
| **Operational Metrics** | fact_delivery_performance | Jan-Sep 2025 | 149K delivery logs | actual_delivery_time_mins, expected_delivery_time_mins, distance_km |
| **Menu & Order Items** | dim_menu_item, fact_order_items | Jan-Sep 2025 | 343K menu items, 343K order lines | menu_item_id, quantity, line_total |

### Key Fields & Definitions

**Phase Classification:**
- **Pre-Crisis:** January - May 2025 (5 months baseline)
- **Crisis:** June - September 2025 (4 months of operational failure)

**Customer Segmentation:**
```
Total Customers:      105K  (all unique customers who placed at least one order)
Active:               100K  (at least one non-cancelled order)
Churned:               73K  (orders pre-crisis, ZERO orders in crisis)
New:                   18K  (first order in Jun-Sep 2025)
Retained:              14K  (orders in both periods)
Loyal:                  50  (5+ non-cancelled pre-crisis orders)
```
Customers who ordered in Jan-May: 86,824. Customers who ordered in Jun-Sep: 32,412.

**Order Metrics:**
```
Pre-Crisis Total:             113,806 orders  (~22.8K per month)
Crisis Total:                  35,360 orders  (~8.8K per month)
Order Frequency Drop:                     69%  (total vs total)
Monthly Average Decline:                  61%  (22.8K → 8.8K per month)
```

**Revenue Metrics:**
```
Pre-Crisis Total:      ₹3.76 Cr  (₹37.62M, 5 months)
Crisis Total:          ₹1.09 Cr  (₹10.94M, 4 months)
Difference:            ₹2.67 Cr lost (₹26.68M)
Decline:               70.92%
```

---

## 🔬 Methodology

### 1. Data Analysis Framework

#### A. Descriptive Analysis
**Purpose:** Understand current state and crisis severity

**Metrics Calculated:**
- Order volume by month, city, cuisine and partner type
- Revenue by component (subtotal, delivery fee, discounts)
- Customer counts by status (active, churned, new, retained, loyal)
- Cancellation rates and SLA compliance trends
- Average ratings, sentiment scores and review themes

**Tools:** Power BI aggregations and DAX measures

#### B. Comparative Analysis
**Purpose:** Quantify pre-crisis vs crisis changes

**Methodology:**
```
Decline % = (Pre-Crisis Value - Crisis Value) / Pre-Crisis Value × 100

Example - Order Frequency Drop:
= (113,806 - 35,360) / 113,806 × 100
= 68.93% decline
```
Pre-crisis covers 5 months and crisis covers 4, so total-to-total declines are larger than month-to-month declines (69% vs 61% for orders).

**Applied to:** Orders, revenue, ratings, cancellations, SLA compliance, delivery time

#### C. Customer Segmentation
**Purpose:** Identify recoverable customers

**Customer status** (Page 3): Churned, Retained, New, Other, based on completed orders in each phase.

**Return segments** (Page 8), assigned per customer and shown as order counts:

**Active Customers:** at least one order in the crisis period  
Orders: 53.72K (36.01%)

**High Return:**
```
IF (Pre-Crisis Orders ≥ 5) AND (Avg Rating > 4.5) AND (Crisis Orders = 0)
THEN "High Return"
```
Orders: ~0.13K | Customers: 26 loyal, high-rated customers who left

**Medium Return:**
```
IF (Pre-Crisis Orders ≥ 3) AND (Avg Rating > 3.5) AND (Crisis Orders = 0)
THEN "Medium Return"
```
Orders: 9.12K (6.12%)

**Low Return:** all remaining customers who left  
Orders: 86.19K (57.78%)

Return probability percentages: **NA** (not modelled).

#### D. Revenue Impact Analysis
**Purpose:** Quantify financial loss across components

**Revenue Breakdown:**
```
Total Net Revenue = Subtotal Amount + Delivery Fee - Discounts Applied

Pre-Crisis Subtotal:      ₹36.34M
Crisis Subtotal:          ₹10.56M
Subtotal Decline:         70.95%

Pre-Crisis Delivery Fee:  ₹3.47M
Crisis Delivery Fee:      ₹1.01M
Delivery Fee Decline:     70.84%

Pre-Crisis Discounts:     ₹2.19M
Crisis Discounts:         ₹0.63M
Discount Decline:         71.34%

Total Net Revenue:        ₹37.62M → ₹10.94M
Total Revenue Lost:       ₹26.68M (70.92% decline)
```

#### E. Sentiment Analysis
**Purpose:** Understand customer perception changes

**Sentiment Scoring Method:**
The dataset provides a sentiment score from -1 to +1 for each review.
```
Score ≥ 0.3:        Positive
Score -0.3 to 0.3:  Neutral
Score < -0.3:       Negative

Pre-Crisis Avg Rating:    4.50  → Positive sentiment (avg score 0.75)
Crisis Avg Rating:        2.50  → Negative sentiment (avg score -0.25)
Sentiment Change:         -1.00 on the -1 to +1 scale
```

**Keyword Analysis:**
- Review text themes counted across 69K reviews
- Frequency analysis of negative themes (sentiment score below 0)
- Themes grouped into quality/safety, delivery and pricing issues
- Crisis vs pre-crisis comparison

**Top negative review themes during the crisis:**

| Review theme | Reviews |
|---|---|
| Food quality is not good | 1,596 |
| Food safety issue | 1,076 |
| Packaging issue | 997 |
| Bad taste | 972 |
| Stale food served | 971 |
| Not recommended | 942 |
| Very late | 904 |
| Cold food | 668 |
| Portion size smaller than expected | 658 |
| Not worth the price | 655 |

---

### 2. Customer Acquisition Cost (CAC) Analysis

```
CAC = Total Marketing Spend / Number of New Customers Acquired
Pre-Crisis CAC:   NA
Crisis CAC:       NA
Increase:         NA
```

| Factor | Impact | Source |
|--------|--------|--------|
| GST implementation | NA | NA |
| Advertising cost increase | NA | NA |
| Monsoon seasonality | NA | NA |
| Brand reputation damage | NA | NA |

The dataset has no marketing spend, so CAC was not analysed. What it does show: 18K new customers were acquired in the crisis period, against 73K churned.

---

### 3. Recovery Strategy Modeling

#### Recovery Potential Model (Page 8)
```
Recovery = Lost Revenue × (1 - Churn Rate) × Sentiment Factor

Lost Revenue     = Pre-Crisis Revenue - Crisis Revenue (per city)
Churn Rate       = Customers Lost / Pre-Crisis Customers
Customers Lost   = Customers who ordered pre-crisis - Customers who ordered in crisis
Sentiment Factor = 0.8 if the city's average crisis rating < 2.5, else 1.0
```

| City | Tier | Market Size (pre-crisis orders) | Revenue Lost | Customers Lost | Recovery Potential |
|---|---|---|---|---|---|
| Bengaluru | Tier-1 | 31,277 | ₹7.59M | 15,170 | ₹2,173,321 |
| Mumbai | Tier-1 | 17,848 | ₹4.34M | 8,622 | ₹1,250,435 |
| Delhi | Tier-1 | 15,580 | ₹3.73M | 7,474 | ₹1,352,959 |
| Hyderabad | Tier-2 | 10,855 | ₹2.60M | 5,236 | ₹958,537 |
| Chennai | Tier-2 | 11,046 | ₹2.60M | 5,150 | ₹794,054 |
| Pune | Tier-2 | 8,817 | ₹2.12M | 4,225 | ₹618,725 |
| Ahmedabad | Tier-3 | 7,648 | ₹1.86M | 3,685 | ₹684,837 |
| Kolkata | Tier-3 | 7,601 | ₹1.85M | 3,667 | ₹677,637 |
| **Total** | | | **₹26.68M** | **53,229** | **~₹8.51M** |

Tier-1 cities account for about 59% of the lost revenue and 56% of the recovery potential.

#### Recovery pillars
| Pillar | Investment | Expected Impact | Timeline |
|---|---|---|---|
| Delivery reliability and SLA | NA | NA | NA |
| Food safety monitoring | NA | NA | NA |
| Customer win-back | NA | NA | NA |
| Restaurant support | NA | NA | NA |
| **Total roadmap** | NA | NA | NA |

---

### 4. Competitive Benchmarking

| Competitor | Market Share | Revenue Growth | Strategy |
|---|---|---|---|
| Zomato | NA | NA | NA |
| Swiggy | NA | NA | NA |

Competitor analysis was outside the scope of this dashboard.

---

## 📈 Key Findings

### Crisis Impact Summary

| Metric | Pre-Crisis | Crisis | Change | % Change |
|--------|-----------|--------|--------|----------|
| Total Orders (period) | 113,806 | 35,360 | -78,446 | -68.9% |
| Avg Monthly Orders | ~22.8K | ~8.8K | -~13.9K | -61.2% |
| Avg Monthly Revenue | ₹7.52M | ₹2.74M | -₹4.78M | -63.7% |
| Total Revenue (period) | ₹37.62M (₹3.76 Cr) | ₹10.94M (₹1.09 Cr) | -₹26.68M | -70.9% |
| Customers Ordering | 86,824 | 32,412 | -54,412 | -62.7% |
| Avg Rating | 4.50 | 2.50 | -2.00 | -44.5% |
| Avg Sentiment Score | 0.75 | -0.25 | -1.00 | NA |
| SLA Compliance | 43.6% | 12.2% | -31.4 pts | -72% |
| Avg Delivery Time | 39.5 min | 60.1 min | +20.6 min | +52% |
| Avg SLA Delay | 2.02 min | 17.60 min | +15.58 min | 8.7× |
| Cancellation Rate | 6.06% | 11.93% | +5.87 pts | +97% |
| Active Restaurants (per month) | ~13.1K | ~6.5K | -~6.6K | -50.7% |
| Reviews (per month) | ~10.7K | ~3.9K | -~6.8K | -63.7% |

### Root Causes

**Primary (Operational):**
1. SLA compliance collapsed 44% → 12%
2. Average delivery time jumped from ~40 to 60 minutes, and delays grew 8.7×
3. Cancellations roughly doubled (6.06% → 11.93%), highest in Bengaluru (7.19%), Kolkata (7.14%) and Chennai (7.04%) during the crisis

**Secondary (Reputational):**
1. Viral food safety incident (case background)
2. Share of negative reviews climbed from 34.68% (June) to 53.45% (September)
3. Top complaints: Quality (1,596), Safety (1,076), Packaging (997)

**Tertiary (Competitive):**
- Competitor campaigns (case background). Customers lost to competitors: **NA**

**External (Market):**
- Monsoon-season delivery outage (case background). GST and advertising-cost effects: **NA**

### Customer & Partner Findings

- **Uniform decline:** every city fell 68-70% (Bengaluru 70.23%, Mumbai 70.18%, Ahmedabad 69.89%, Pune 69.81%, Delhi 69.81%) and every cuisine fell 68.5-70.3%.
- **Top 5% (VIP) customers:** 5K VIPs (spend of ₹877+ in Jan-May). Their average spend fell 97% in the crisis, their order frequency dropped from 2.6 to 1.1 orders, and ₹0.58 Cr of their pre-crisis revenue is at risk (about ₹1.4 Cr annualised). 84% of VIPs placed no orders in the crisis.
- **Loyal customers:** only 50 customers had 5+ completed pre-crisis orders, and 26 high-rated loyal customers left.
- **Partners:** retention rate 0.79 (15.7K of 20K restaurants active in both periods). Cloud kitchens (6K) fell 68.60% vs 69.07% for restaurants (14K). Restaurants with 10-19 pre-crisis orders fell 85.6% vs 69.3% for those with fewer than 10, though grouping by pre-crisis volume exaggerates this gap.
- **Order value:** premium orders (₹140+) fell 70.89%.

### Recovery Opportunity

**Recoverable Customer Base:**
- Total recovery potential: ~₹8.51M (about 32% of lost revenue)
- Highest potential: Bengaluru ₹2.17M, Delhi ₹1.35M, Mumbai ₹1.25M
- Geographic concentration: Bengaluru (27% of orders, 29% of VIPs) and Mumbai (16% of orders)
- High-priority loyal customers: 26 (60% recovery probability: **NA**)

**Key Insight:**
Customers did not leave because of a preference shift. They left because of service failure: the decline was identical across cities and cuisines, while SLA, delivery time and cancellations all deteriorated at the same moment. This is reversible through operational fixes plus targeted win-back.

### Data Notes & Limitations
- Pre-crisis is 5 months and crisis is 4, so total-to-total declines (69%) are larger than monthly-average declines (61%).
- 5,053 orders (all cancelled) belong to customers missing from the customer table. They count in the order totals, but have no city, so the city-level cancellation chart excludes them.
- Restaurant names repeat across restaurants (for example "Urban Kitchen Zone" is 8 outlets), so the Page 6 table is by name, not by individual outlet.
- The donuts on Pages 3 and 8 count orders, not unique customers.
- The cuisine chart and the monthly average spend line on Page 4 show all customers, not only VIPs.
- The "Budget" price tier is almost entirely cancelled orders (6,894 of 6,905 pre-crisis orders have a ₹0 value).
- The sentiment factor in the recovery model flips at an average crisis rating of 2.5, and city ratings span only 2.48-2.55, so city-level recovery figures are indicative.

---

## 💡 Recommendations

### Immediate Actions (Month 1)

1. **Launch a VIP and win-back campaign**
   - Target: 5K top-5% VIPs (₹0.58 Cr pre-crisis revenue at risk) and lapsed customers in Bengaluru, Delhi and Mumbai
   - Offer: **NA**
   - Expected: **NA**

2. **Strengthen food safety monitoring across partner restaurants**
   - Address the top complaints: quality (1,596), safety (1,076), packaging (997), stale food (971)
   - Visible hygiene standards for partners
   - Expected: **NA**

3. **Restaurant Support Program**
   - Focus on small and low-volume restaurants (Tiny: 96.8K → 29.7K orders) and cloud kitchens (-68.60%)
   - Expected retention uplift: **NA**

### Medium-term (Month 2-6)

4. **Delivery reliability and SLA overhaul**
   - Prioritise Bengaluru, Kolkata and Chennai (highest crisis cancellation rates)
   - Real-time SLA monitoring (SLA fell 44% → 12%)
   - Fleet allocation and weather-adaptive routing for monsoon periods

5. **Customer Retention Program**
   - Tiered loyalty benefits for repeat customers
   - Regular engagement campaigns
   - Feedback loops built on the sentiment dashboard

### Long-term (Month 6-9)

6. **Market Repositioning**
   - Competitive differentiation based on reliability
   - Recover Tier-1 cities first (56% of recovery potential), then Tier-2 and Tier-3
   - Total investment, timeline and ROI: **NA**

---

## 🛠️ Technical Implementation

### Tools & Technologies Used

**Data Visualization:**
- **Power BI Desktop:** Interactive dashboard, 8 pages
- **Visual Types:** Cards, line and column charts, bar charts, donut charts, area chart, tables, matrix, word cloud
- **DAX Functions:** CALCULATE, SWITCH, IF, DIVIDE, DISTINCTCOUNT, FILTER, VALUES, ADDCOLUMNS, TOPN, ALLEXCEPT, PERCENTILE.INC, AVERAGEX, SUMX

**Data Analysis:**
- **DAX Measures:** ~40 custom measures for segmentation, SLA, risk scoring and recovery potential
- **Calculated Columns and Tables:** ~11 calculated columns (for example Customer_Status, VIP_Segment, Risk_Level, Return_Segment, Time_Bucket) and a calculated date table
- **Modeling:** Star schema across 8 tables with a Dim_Date table driving the pre-crisis and crisis phases

### Dashboard Structure

**Page 1: Home**
- Quick navigation to all analysis sections
![Page 1: Home](<img width="1157" height="653" alt="image" src="https://github.com/user-attachments/assets/86a3a0c9-9879-4344-8aa3-0cfe8a1bcf5b" />)

**Page 2: Executive Summary (Crisis Overview)**
- KPI cards: total orders (149K), average rating (4.05), cancellation rate (7.45%), order frequency drop (69%), pre-crisis and crisis revenue (₹3.76 Cr and ₹1.09 Cr)
- Monthly revenue and order/cancellation trend
- Top cities by order decline
- Revenue breakdown by component
![Page 2: Executive Summary](<img width="579" height="328" alt="Page 2" src="https://github.com/user-attachments/assets/b9142c85-0776-4471-b1d1-7bd123b693c0" />
)

**Page 3: Customer Impact Analysis**
- Customer status KPIs: 105K total, 100K active, 50 loyal, 73K churned, 18K new, 14K retained
- Orders by city and by customer status
- Loyal customers who left (5+ pre-crisis orders, none in the crisis)
![Page 3: Customer Impact Analysis](<img width="581" height="327" alt="Page 3" src="https://github.com/user-attachments/assets/1fc52ec0-8090-44ef-9ed5-dbbbc382ac51" />
)

**Page 4: Top 5% Spent Customer Impact**
- VIP metrics: 5K VIPs, ₹0.58 Cr revenue at risk, -0.97 average decline, 0.02 cancellation rate, 2.64 churned average delay
- VIP order frequency (2.6 → 1.1) and city distribution
- Cuisine preferences and monthly spend
![Page 4: Top 5% Spent Customer Impact](<img width="578" height="326" alt="Page 4" src="https://github.com/user-attachments/assets/55cd86f1-2d77-48ce-9361-185b7636350e" />
)

**Page 5: Operational Performance**
- KPIs: average SLA delay 5.71 minutes, SLA compliance 36%, SLA drop 0.31, delay increase 15.58 minutes, 15K delivery partners, 10 deliveries per partner, top city Bengaluru
- SLA compliance and delivery time by month
- Cancellation rates by city and phase, SLA by vehicle type and time bucket
![Page 5: Operational Performance](<img width="580" height="327" alt="Page 5" src="https://github.com/user-attachments/assets/9fd3a040-cadd-48ed-b813-bb55a820d718" />
)

**Page 6: Restaurant Partnership Analysis**
- KPIs: 20K partner restaurants, 6K cloud kitchens, 16K active in both periods, 0.79 retention rate, 14K restaurants
- City retention rates and cuisine-wise order comparison
- Restaurant risk levels and top declining restaurants
- Active restaurants by month
![Page 6: Restaurant Partnership Analysis](<img width="579" height="326" alt="Page 6" src="https://github.com/user-attachments/assets/e2a39dcc-0c9c-46c2-a8bd-6c5c0fb57e9f" />
)

**Page 7: Customer Sentiment Analysis**
- Rating trend (4.6 → 2.3) and average sentiment trend (0.79 → -0.35)
- Review volume by sentiment category
- Negative review word cloud and top negative themes
![Page 7: Customer Sentiment Analysis](<img width="579" height="327" alt="Page 7" src="https://github.com/user-attachments/assets/2272140c-7728-4ea1-9aa5-b8f446cc412e" />
)

**Page 8: Additional Insights**
- Orders by partner type (cloud kitchen vs restaurant) and restaurant size
- Average SLA delay vs % negative reviews by month
- Loss and recovery potential by city tier
- Return segments and orders by price tier
![Page 8: Additional Insights](<img width="577" height="325" alt="Page 8" src="https://github.com/user-attachments/assets/e4fa1153-1114-4afa-acfe-387be3ba8d16" />
)

---

## 📦 Deliverables

| Deliverable | Status |
|---|---|
| Power BI dashboard (.pbix), 8 pages | ✅ |
| Dashboard screenshots | ✅ |
| README documentation | ✅ |
| Presentation / video walkthrough | NA |

---

## 📚 Sources & References

### External Research
- No external research was used. All numbers are calculated from the Codebasics Resume Project Challenge dataset.
- Competitor market share, GST impact, food safety certification and cloud kitchen market sources: **NA**

### Methodology References

#### Statistical Analysis
- **Churn Modeling:** Customers with orders pre-crisis and zero orders in the crisis
- **Risk Scoring:** Rule-based restaurant risk levels from order decline (Critical 80%+, High 50-79%, Medium 20-49%, Low under 20%)
- **Recovery Estimation:** Lost revenue × (1 - churn) × sentiment factor
- **Probability Assessment:** **NA**

#### Data Analysis Best Practices
- **Comparative Analysis:** Pre/post crisis methodology
- **Customer Segmentation:** Rule-based behavioral segments
- **Sentiment Analysis:** Review theme frequency analysis with sentiment score categories
- **Benchmark Validation:** **NA**

---

## 🔍 How to Explore

**Customer Analysis:**
- Page 3 (Customer Impact) + Page 4 (VIP Impact)
- Segmentation criteria
- Recovery opportunity identification

**Operational Insights:**
- Page 5 (Operational Performance)
- SLA and delivery metrics
- Root cause of cancellations

**Strategic Understanding:**
- Page 8 (Additional Insights)
- Restaurant churn analysis, return segments and recovery potential
- Order value shifts

---

## 📊 Key Metrics Summary

| Category | Metric | Value | Context |
|----------|--------|-------|---------|
| **Orders** | Pre-Crisis Total | 113,806 | 5 months (~22.8K per month) |
| | Crisis Total | 35,360 | 4 months (~8.8K per month) |
| | Order Frequency Drop | 69% | Total vs total |
| **Revenue** | Pre-Crisis Total | ₹3.76 Cr | 5-month period |
| | Crisis Total | ₹1.09 Cr | 4-month period |
| | Loss | ₹2.67 Cr | 70.92% decline |
| **Customers** | Total | 105K | Placed at least one order |
| | Churned | 73K | Lost customers |
| | New / Retained | 18K / 14K | Crisis period |
| | Loyal (5+ orders) | 50 | High-priority win-back |
| **Ratings** | Pre-Crisis | 4.50 stars | Strong satisfaction |
| | Crisis | 2.50 stars | Critical deterioration |
| | Overall | 4.05 stars | Jan-Sep average |
| **Operations** | SLA Pre → Crisis | 44% → 12% | Failure |
| | Delivery Time | 40 → 60 min | +50% |
| | Cancellation Rate | 6.1% → 11.9% | Roughly doubled |
| **Partners** | Retention Rate | 0.79 | Active in both periods |
| **Recovery** | Recovery Potential | ~₹8.51M | ~32% of lost revenue |
| | Investment / ROI | NA | Not modelled |

---

## ❓ FAQ

**Q: How was customer churn calculated?**  
A: Customers who placed at least one order in the pre-crisis period (Jan-May) but zero orders in the crisis (Jun-Sep). Result: 72,768 (73K) churned. That is 73% of the 100K active customers, 69% of all 105K customers, and 84% of the 86,824 who ordered pre-crisis.

**Q: Why are so few customers marked as loyal or high-return?**  
A: Order frequency in this dataset is low (most customers placed only one or two orders). Only 50 customers had 5+ completed pre-crisis orders, and 26 of the loyal customers who left had an average rating above 4.5.

**Q: How reliable is the recovery potential figure?**  
A: It is a rule-based estimate, not a forecast. The sentiment factor drops to 0.8 for cities with an average crisis rating below 2.5, and all cities sit between 2.48 and 2.55, so the city ranking should be read as indicative.

**Q: What external data was used?**  
A: None. Every figure comes from the dataset's eight tables.

**Q: Can this analysis be adapted?**  
A: Yes. The framework (phase split, status segments, SLA and sentiment analysis) transfers to other food delivery or e-commerce crisis scenarios.

---

## 🔗 Related Resources

- **Power BI Report:** `[add your published Power BI link]`
- **LinkedIn Post:** `[add your LinkedIn post link]`
- **Contact:** `[add your LinkedIn profile]` | `[add your email]`

---
