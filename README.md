
# 📊 RFM Customer Segmentation Analysis — Power BI Dashboard

> **Transforming transactional data into strategic customer intelligence** — A 2-page interactive Power BI report built on the Superstore dataset that applies RFM (Recency, Frequency, Monetary) scoring to segment customers, track active vs. inactive behaviour by state, and benchmark segment-level profitability and revenue contribution.

---

## 🔍 Project Overview

This Power BI dashboard answers three critical business questions:

1. **Who are our most valuable customers right now?** (Champions, At-Risk counts, Lifetime Value, Repeat Rate)
2. **How are customer segments performing?** (Revenue% and Profit% by Customer_segment, Average Revenue per segment)
3. **Where are we losing customers?** (Active vs. Inactive customers by state + cumulative % trend)

The report uses **RFM scoring logic** (Recency, Frequency, Monetary) to assign each customer a composite score, then groups them into actionable segments — enabling marketing, sales, and CX teams to prioritise effort based on data, not instinct.

---

## 📁 Report Structure

### Page 1 — Overview

| Visual | Metric | Purpose |
|---|---|---|
| KPI Card | **Total Customers** | Baseline headcount |
| KPI Card | **Champion Customers** | High R+F+M score count |
| KPI Card | **At-Risk Customers** | Previously active, now lapsing |
| KPI Card | **Customer Lifetime Value (CLV)** | Average revenue over customer lifespan |
| KPI Card | **Repeat Rate** | % of customers who returned for a 2nd+ purchase |
| Matrix   | **R Score × F Score matrix** | Cross-tab of Recency and Frequency scores showing customer count per cell — maps the full RFM distribution |

(dashboard.png)<[https://github.com/deepikadhondiyal-analyst/RFM-Analysis/blob/main/Screenshot%202026-06-01%20135441.png] />


### Page 2 — Customer Behavior Analysis

| Visual | Metric | Purpose |
|---|---|---|
| Combo Chart (Bar + Line) | **Active vs. Inactive Customers by State + Cumulative %** | Geographic breakdown of engagement with running total |
| Bar Chart | **Average Revenue by Segment** | Revenue productivity per segment |
| Column Chart (Bookmark: Revenue) | **Revenue% by Customer Segment** | Revenue share contributed by each Customer_segment |
| Column Chart (Bookmark: Profit) | **Profit% by Customer Segment** | Profitability contribution by each Customer_segment |

> **Bookmarks** allow the user to toggle between Revenue view and Profit view on the same chart space — a clean UX pattern for executive reporting.

---


## 🧮 RFM Scoring Framework [Excel]

| Dimension | Definition | Score Signal |
|---|---|---|
| **Recency (R)** | How recently did the customer purchase? | Higher = bought more recently |
| **Frequency (F)** | How many times have they purchased? | Higher = more transactions |
| **Monetary (M)** | How much total revenue have they generated? | Higher = more spend |

Customers are scored on each dimension and the **Rf_score** (combined Recency + Frequency composite) is used in the matrix on the Overview page to map the distribution of the customer base across engagement levels.

### Segment Definitions

| Segment | RFM Profile | Recommended Action |
|---|---|---|
| 🏆 **Champions** | High R, High F, High M | Reward, upsell, use as brand advocates |
| 🟢 **Loyal** | High F & M, moderate R | Nurture loyalty programs |
| ⚠️ **At-Risk** | Was high F/M, R declining | Immediate win-back campaign |
| 🔴 **Inactive / Lost** | Low R, Low F | Re-engagement or deprioritise |

---



## 🛠️ Tools & Technologies

| Tool | Usage |
|---|---|
| **Microsoft Power BI Desktop** | Data modelling, DAX, report design |
| **DAX** | Custom measures: `Total_Customer`, `Champion_Customer`, `At-Risk_Customer`, `Lifetime_Value`, `Repeat_Rate`, `Active_Customer`, `Inactive_Customers`, `Cumulative%`, `Avg_Revenue`, `Revenue%`, `Profit%` |
| **Power Query (M)** | Data transformation, cleaning, column derivation |
| **Sample Superstore Dataset** | Transactional sales data (Orders, Customers, Segments, States) |
| **Bookmarks** | Toggle between Revenue and Profit views on Customer Behavior page |

---

## 📐 Key DAX Measures (Conceptual)

```dax
-- Total unique customers
Total_Customer = DISTINCTCOUNT('Sample_ Superstore'[Customer ID])

-- Champion customers (top RFM tier)
Champion_Customer = 
CALCULATE(
    [Total_Customer],
    'Measure'[Rf_score] = <top_tier_threshold>
)

-- At-Risk customers (high past frequency, declining recency)
At-Risk_Customer = 
CALCULATE(
    [Total_Customer],
    <at_risk_segment_filter>
)

-- Customer Lifetime Value
Lifetime_Value = DIVIDE([Total Revenue], [Total_Customer])

-- Repeat Purchase Rate
Repeat_Rate = 
DIVIDE(
    COUNTROWS(FILTER(customer_orders, order_count > 1)),
    [Total_Customer]
)

-- Cumulative % (for combo chart)
Cumulative% = 
DIVIDE(
    CALCULATE([Active_Customer], ALLSELECTED()),
    [Total_Customer]
)
```

---

## 💼 Business Impact

- **Champion identification**: Instantly surfaces the highest-value customer tier — enabling marketing to allocate retention budget where ROI is highest
- **At-Risk early warning**: Flags customers showing recency decline before they churn, creating a window for proactive win-back
- **Geographic engagement gaps**: Active vs. Inactive by State reveals where customer engagement is weakest — actionable for regional sales strategy
- **Segment-level P&L**: Revenue% vs Profit% by segment exposes which segments drive volume vs. which drive actual margin — critical for pricing and discount strategy
- **Repeat Rate KPI**: A single metric that benchmarks loyalty program effectiveness over time



---

## 👤 Author

**[Deepika Dhondiyal]**  
Data Analyst | Power BI | DAX | SQL | Excel
[LinkedIn](www.linkedin.com/in/deepikadhondiyalofficial)

---
