# FUTURE_DS_03: E-Commerce Conversion Funnel & Customer Journey Analytics

![Power BI](https://img.shields.io/badge/Power_BI-F2C811?style=for-the-badge&logo=powerbi&logoColor=black)
![DAX](https://img.shields.io/badge/DAX-Data_Analysis_Expressions-blue?style=for-the-badge)
![Status](https://img.shields.io/badge/Status-Completed-success?style=for-the-badge)

An interactive, enterprise-grade Power BI business intelligence dashboard tracking user engagement across the full acquisition and conversion funnel. This solution identifies critical drop-off stages, evaluates cross-channel and device performance, and translates e-commerce behavioral event telemetry into actionable operational strategies[cite: 16].

---

## 📌 Table of Contents
1. [Project Overview](#-project-overview)
2. [Dataset & Data Architecture](#-dataset--data-architecture)
3. [Key Performance Indicators (KPIs)](#-key-performance-indicators-kpis)
4. [Dashboard Architecture & Previews](#-dashboard-architecture--previews)
5. [Complete DAX Measures & Calculations](#-complete-dax-measures--calculations)
6. [Business Insights & Operational Actions](#-business-insights--operational-actions)
7. [Tools & Technologies Used](#-tools--technologies-used)
8. [Repository Structure](#-repository-structure)
9. [Setup & Reproduction Guide](#-setup--reproduction-guide)

---

## 📌 Project Overview

Digital conversion funnels in e-commerce frequently suffer from significant blind spots between top-of-funnel discovery and transaction completion[cite: 11]. This project analyzes **12,000 recorded user events** across **5,128 unique users/sessions** covering the full calendar year of 2024 (January 1, 2024 to December 30, 2024)[cite: 16].

### Primary Analytical Goals:
* **Quantify Conversion Velocity:** Measure step-by-step conversion from discovery (`Product_View` + `Search_Click`) to intent (`Cart_Add`) and purchase (`Purchase`)[cite: 11].
* **Identify Device & Channel Discrepancies:** Isolate conversion friction across mobile, desktop, and tablet platforms[cite: 12].
* **Diagnose Margin & Leakage Points:** Evaluate discount thresholds and quantify revenue loss tied to out-of-stock items and cart abandonment.

---

## 📁 Dataset & Data Architecture

The underlying dataset contains e-commerce transaction and interaction telemetry across the following schema:

* **Event Identifiers:** `User_ID`, `Session_ID`, `Product_ID`, `Brand_ID`, `Timestamp`
* **Funnel Telemetry:** `Event_Type` (`Product_View`, `Search_Click`, `Cart_Add`, `Wishlist_Add`, `Purchase`)[cite: 11]
* **User Demographics & Segments:** `User_Region`, `User_Age_Group`, `Membership_Type` (`Regular`, `Silver`, `Gold`, `Premium`)
* **Traffic & Hardware:** `Traffic_Source` (`Direct`, `Search_Engine`, `Social_Media`, `Advertisement`, `Email`), `Device_Type` (`Mobile`, `Desktop`, `Tablet`)[cite: 6, 16]
* **Product Catalog:** `Category_Name` (10 Categories), `Product_Price`, `Discount_Percent`, `Stock_Status` (`In_Stock`, `Limited_Stock`, `Out_of_Stock`)[cite: 6, 18]

---

## 📊 Key Performance Indicators (KPIs)

| KPI Metric | Baseline Value | Calculation Formula | Strategic Context |
| :--- | :---: | :--- | :--- |
| **Browsing Events** | **7,430** | $\text{Product Views } (4,951) + \text{Search Clicks } (2,479)$ | Total high-intent top-of-funnel interactions[cite: 11, 16] |
| **Cart Adds** | **2,078** | $\text{COUNTROWS}(\text{Event\_Type} = \text{"Cart\_Add"})$ | Mid-funnel purchase intent volume[cite: 16] |
| **Purchases** | **951** | $\text{COUNTROWS}(\text{Event\_Type} = \text{"Purchase"})$ | Completed bottom-of-funnel transactions[cite: 16] |
| **Cart Rate** | **27.97%** | $\frac{\text{Cart Adds}}{\text{Browsing Events}}$ | Platform-wide interest-to-cart progression rate[cite: 16] |
| **Cart to Purchase** | **45.77%** | $\frac{\text{Purchases}}{\text{Cart Adds}}$ | Final checkout conversion efficiency[cite: 16] |
| **Avg Order Value (AOV)** | **₹29,443** | $\frac{\sum(\text{Product Price} \times (1 - \text{Discount}))}{\text{Purchases}}$ | Net realized revenue per completed order[cite: 16] |

---

## 🖥️ Dashboard Architecture & Previews

### Page 1: Funnel Overview
![Funnel Overview](Screenshot%202026-10-21%20173428.png)

* **Interactive Slicer Pane:** Features dark button tiles for Device, Membership, Region, Age Group, Discount Band, and Stock Status, alongside a dedicated "Clear all" button[cite: 6, 16].
* **Funnel (Browsing to Purchase):** Custom funnel visual tracking progression from 7,430 browsing events down to 2,078 cart adds (28.0%) and 951 purchases (45.8%)[cite: 11, 16]. Flags **1,541 Wishlist adds (20.7% of browsing)** as an isolated remarketing pool outside the funnel[cite: 11, 16].
* **Event Mix (Donut Chart):** Proportional distribution of 12,000 total events: Product Views (41.3%), Search Clicks (20.7%), Cart Adds (17.3%), Wishlist Adds (12.8%), and Purchases (7.9%)[cite: 11, 16].
* **Cart to Purchase Gauge:** Visual radial dial benchmarking actual close rate (45.8%) against target scale ($0\%\text{--}100\%$)[cite: 11, 16].
* **Conversion by Month:** Longitudinal dual-line chart tracking Cart Rate ($22\%\text{--}31\%$) and Cart to Purchase ($36\%\text{--}56\%$) across all 12 calendar months[cite: 12, 16].
* **Events Mix by Device:** 100% horizontal stacked segmentation across **Mobile** (7,084 events), **Desktop** (3,898 events), and **Tablet** (1,018 events)[cite: 12, 16].

---

### Page 2: Segments Deep-Dive
![Segments Deep-Dive](Screenshot%202026-10-21%20173449.png)

* **Conversion by Segment (Field Parameter):** Clustered bar chart driven by a single-select parameter dropdown (`Traffic Source`, `Device`, `Membership`, `Region`, `Age Group`, `Stock Status`)[cite: 13, 14, 17].
* **Purchases by Category (Treemap):** Two-variable encoding where tile area represents completed purchase volume and color gradient represents checkout efficiency ($38.9\%$ to $57.2\%$) with a lower-to-higher scale[cite: 13, 17].
* **Channel by Device Matrix Heatmap:** Cross-tabulates traffic sources against hardware platforms, rendering conversion rates alongside cart volumes with statistical low-sample flags (`*` for groups $<30$ carts)[cite: 13, 17, 18].
* **Category Detail Table:** Granular operational summary with embedded data bars tracking category performance from Grocery ($115$ orders, $57.2\%$ close rate) to Toys ($79$ orders, $38.9\%$ close rate)[cite: 17, 18].

---

### Page 3: Strategic Insights & Recommendations
![Strategic Insights](Screenshot%202026-10-21%20173506.png)

* **Executive Summary Grid:** $4 \times 2$ structured analytical takeaway cards classifying findings into statistical tests (`TESTED`), business directions (`DIRECTIONAL`), and operational checks (`DATA QUALITY`)[cite: 18].
* **Methodology Banner:** Formal analytical transparency statement explaining funnel event modeling, session deduplication caveats, and statistical parameters.

---




## 📐 Complete DAX Measures & Calculations
```dax
All DAX formulas utilized in building this analytics dashboard are detailed below:

### 1. Base Event & Volume Counts

-- Total platform interactions
Total Events = 
COUNTROWS('ecommerce dataset')

Browsing Events = 
CALCULATE(
    COUNTROWS('ecommerce dataset'),
    'ecommerce dataset'[Event_Type] IN { "Product_View", "Search_Click" }
)


Cart Adds = 
CALCULATE(
    COUNTROWS('ecommerce dataset'),
    'ecommerce dataset'[Event_Type] = "Cart_Add"
)

Purchases = 
CALCULATE(
    COUNTROWS('ecommerce dataset'),
    'ecommerce dataset'[Event_Type] = "Purchase"
)


Cart Rate = 
DIVIDE( [Cart Adds], [Browsing Events], 0 )


Cart to Purchase = 
DIVIDE( [Purchases], [Cart Adds], 0 )


Avg Order Value = 
VAR _NetRevenue = 
    SUMX(
        FILTER('ecommerce dataset', 'ecommerce dataset'[Event_Type] = "Purchase"),
        'ecommerce dataset'[Product_Price] * (1 - ('ecommerce dataset'[Discount_Percent] / 100))
    )
RETURN
DIVIDE( _NetRevenue, [Purchases], 0 )



---

```
###💡 Business Insights & Operational Actions

1. Funnel Leakage (The Largest Drop-Off)
Data Observation: $54.2\%$ of all cart additions ($1,127$ of $2,078$) result in abandonment without a completed order.

Actionable Next Step: Deploy automated abandoned-cart recovery sequences at $1$-hour and $24$-hour intervals, present guaranteed shipping timelines on the cart drawer, and enable 1-click guest checkout.

2. Device Disparity: Tablet Friction
Data Observation: Tablet cart-to-purchase close rate stands at $38.2\%$, lagging behind Desktop and Mobile ($46.4\%$) by over $8$ percentage points. Purchases per browse on tablet is only $10.2\%$ vs $13.0\%$ platform average.

Actionable Next Step: Conduct immediate QA testing on touch targets, form autofill, and payment iframe responsiveness on tablet viewport dimensions.

3. Promotional Elasticity
Data Observation: The $25\%\text{--}50\%$ discount band achieves the highest checkout close rate ($49.6\%$ vs $43.8\%$ baseline). Items discounted $<10\%$ generate lowest cart additions ($24.2\%$).

Actionable Next Step: Shift low-velocity inventory currently at $<10\%$ discount into the $25\%\text{--}50\%$ promotional bracket; audit whether $50\%\text{--}75\%$ discounts erode gross margin without boosting conversion.

4. Data Hygiene & Inventory Integrity
Data Observation: $1,005$ user events ($8.4\%$) occurred on out-of-stock items, including $164$ cart additions and $75$ completed transactions. Additionally, the recommendation engine fired "Ignore" on $9.0\%$ of sessions.

Actionable Next Step: Enforce real-time inventory checks prior to adding items to cart and suppress zero-stock SKUs from cross-sell widgets.

### 🛠️ Tools & Technologies Used

Business Intelligence & Reporting: Microsoft Power BI Desktop (Latest Version) 

Data Transformation & Modeling: Power Query (M Language) for ETL and data cleansing

Analytics Engine: Data Analysis Expressions (DAX) utilizing context transitions, iterators, and field parameters 

UI/UX Design Framework: Dark Theme (#1E1E1E container background, #118DFF primary accent, #E66C37 secondary accent)  

Statistical Methods: Chi-Square goodness-of-fit testing ($p < 0.05$) to validate statistical significance of conversion gaps


