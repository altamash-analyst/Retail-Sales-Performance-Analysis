# Retail Sales Performance Analysis

![Power BI](https://img.shields.io/badge/Power%20BI-Analytics-yellow)
![Excel](https://img.shields.io/badge/Excel-Data%20Source-green)
![Power Query](https://img.shields.io/badge/Power%20Query-ETL-blue)
![DAX](https://img.shields.io/badge/DAX-Measures-orange)
![Figma](https://img.shields.io/badge/Figma-Design-purple)
![GIMP](https://img.shields.io/badge/GIMP-Graphics-blue)

## Project Overview

**Retail Sales Performance Analysis** is an end-to-end Business Intelligence project developed to analyze retail business performance across sales, profitability, products, customers, regions, order operations, payment methods, and management targets.

The project uses **Excel as the data source**, **Power Query for data preparation**, and **Power BI with DAX for analytical modeling, KPI development, visualization, and business reporting**.

The final solution is designed as a five-page interactive Power BI dashboard that enables users to move from high-level executive performance to detailed product, customer, regional, operational, and target analysis.

### Dashboard Structure

1. **Executive Performance Overview**
2. **Product & Category Performance**
3. **Regional & Customer Performance**
4. **Order & Operations Performance**
5. **Management Performance & Targets**

---

## Business Problem

Retail businesses generate large volumes of transactional and master data across customers, products, regions, orders, and business targets.

The challenge is not simply collecting this data, but converting it into information that management can use to answer practical business questions.

This project addresses questions such as:

- How is overall sales and profitability performing?
- Which products and categories generate the most revenue?
- Which regions are strongest and weakest?
- Which customer segments contribute the most business value?
- What percentage of orders are completed, cancelled, or returned?
- Which payment methods generate the highest sales?
- Are actual sales meeting assigned targets?
- Which regions have the largest target gaps?
- Where should management focus corrective action?

---

## Project Objectives

The main objectives of the project are to:

- Build an interactive retail sales performance dashboard.
- Measure sales, profit, orders, quantity, AOV, and profitability.
- Analyze product and category contribution.
- Compare regional business performance.
- Evaluate customer segment performance.
- Monitor completed, cancelled, and returned orders.
- Analyze payment-method performance.
- Compare actual sales against business targets.
- Identify performance gaps and business risks.
- Convert raw business data into actionable management insights.

---

## Dataset Overview

The project uses confidential retail business data organized across multiple Excel worksheets.

| Dataset | Records | Purpose |
|---|---:|---|
| Orders | 10,000 | Transaction-level sales and order information |
| Customers | 500 | Customer master data |
| Products | 50 | Product and pricing information |
| Regions | 30 | Geographic business information |
| Targets | 600 | Monthly regional sales and profit targets |
| Project Info | Metadata | Project and dataset information |

The analysis is framed around **PY/CY business performance** rather than exposing the underlying confidential source period.

### Data Source

**Source:** Confidential

The source dataset is not publicly identified.

---

# Data Structure

## Orders

The `Orders` table contains transaction-level information.

| Column | Description |
|---|---|
| Order_ID | Unique order identifier |
| Order_Date | Date of the transaction |
| Customer_ID | Customer reference |
| Product_ID | Product reference |
| Region_ID | Region reference |
| Quantity | Quantity purchased |
| Unit_Price | Price per unit |
| Discount | Discount applied |
| Payment_Mode | Payment method |
| Order_Status | Completed, Cancelled, or Returned |

## Customers

The `Customers` table contains customer master information.

| Column | Description |
|---|---|
| Customer_ID | Unique customer identifier |
| Customer_Name | Customer name |
| Gender | Customer gender |
| Age | Customer age |
| City | Customer city |
| State | Customer state |
| Customer_Segment | Consumer, Corporate, or Small Business |
| Registration_Date | Customer registration date |

## Products

The `Products` table contains product and pricing information.

| Column | Description |
|---|---|
| Product_ID | Unique product identifier |
| Product_Name | Product name |
| Category | Product category |
| Sub_Category | Product sub-category |
| Brand | Product brand |
| Cost_Price | Product cost |
| Selling_Price | Product selling price |

## Regions

The `Regions` table contains geographic information.

| Column | Description |
|---|---|
| Region_ID | Unique region identifier |
| Region | Business region |
| State | State |
| City | City |

## Targets

The `Targets` table contains monthly regional business targets.

| Column | Description |
|---|---|
| Month | Target month |
| Region_ID | Region reference |
| Sales_Target | Monthly sales target |
| Profit_Target | Monthly profit target |

---

# Data Preparation

Data preparation was performed using **Power Query** before building the Power BI analytical layer.

### Preparation workflow

```text
Excel Workbook
      |
      v
Power Query
      |
      +--> Data Type Validation
      |
      +--> Column Validation
      |
      +--> Relationship Key Checks
      |
      +--> Data Quality Checks
      |
      +--> Transformation
      |
      v
Power BI Data Model
      |
      v
DAX Measures
      |
      v
Interactive Dashboard
```

### Data Quality Checks

The dataset was reviewed for:

- Missing values
- Duplicate identifiers
- Invalid relationships
- Data-type consistency
- Date consistency
- Product/customer/region key consistency
- Order-status validity
- Target-data consistency

The main datasets contain consistent identifiers and were structured for Power BI analysis.

---

# Data Modeling

The Power BI model connects transactional data with the relevant master and target information.

### Main analytical entities

```text
Customers
    |
    | Customer_ID
    v
Orders ---- Product_ID ----> Products
    |
    | Region_ID
    v
Regions

Targets
    |
    | Region_ID + Month
    v
Regional Target Analysis
```

The model allows transaction-level information to be analyzed by:

- Customer
- Product
- Category
- Region
- Payment Mode
- Order Status
- Time
- Target period

---

# KPI Framework

The dashboard tracks the following major KPIs:

| KPI | Purpose |
|---|---|
| Total Sales | Measures sales value across all order statuses |
| Net Sales | Measures sales from completed orders |
| Total Profit | Measures profit before order-status filtering |
| Net Profit | Measures profit from completed orders |
| Total Orders | Measures transaction volume |
| Completed Orders | Measures successfully completed transactions |
| Total Quantity | Measures units sold |
| Net AOV | Measures average completed-order value |
| Net Profit Margin | Measures profitability relative to net sales |
| Completion Rate | Measures percentage of completed orders |
| Cancellation Rate | Measures percentage of cancelled orders |
| Return Rate | Measures percentage of returned orders |
| Target Achievement | Measures actual performance against target |
| Target Variance | Measures the gap between actual sales and target |

---

# Important Metric Definition

A key distinction in this project is the difference between **Total Sales** and **Net Sales**.

### Total Sales

**Total Sales = ₹302.29M**

This represents sales across all order statuses.

### Net Sales

**Net Sales = ₹273.17M**

This represents sales associated with completed orders.

Therefore:

```text
Total Sales
= Completed Sales
+ Cancelled Sales
+ Returned Sales
```

This distinction is important when interpreting executive KPIs and operational performance.

---

# DAX Analysis

DAX was used to create reusable analytical measures for the Power BI dashboard.

Example calculation structure:

```DAX
Total Sales =
SUMX(
    Orders,
    Orders[Quantity] *
    Orders[Unit_Price] *
    (1 - Orders[Discount])
)
```

```DAX
Total Profit =
SUMX(
    Orders,
    (Orders[Quantity] * Orders[Unit_Price] * (1 - Orders[Discount]))
        - (Orders[Quantity] * RELATED(Products[Cost_Price]))
)
```

The dashboard also uses measures for:

- Net Sales
- Net Profit
- Total Orders
- Completed Orders
- Total Quantity
- Net AOV
- Profit Margin
- Completion Rate
- Cancellation Rate
- Return Rate
- Sales Target
- Target Achievement
- Target Variance
- Regional performance
- Category performance
- Customer-segment performance

---

# Dashboard

## Page 1 — Executive Performance Overview

![Executive Performance Overview](PNG/Dashboard%201.PNG)

The executive dashboard provides a high-level view of business performance.

### Key KPIs

- **Net Sales:** ₹273.17M
- **Net Profit:** ₹67.55M
- **Net Profit Margin:** 24.73%
- **Total Orders:** 10K
- **Total Quantity:** 23K
- **Target Achievement:** 60.20%

### Analysis Areas

- Monthly Sales & Profit Trend
- Sales by Region
- Sales by Category
- Actual Sales vs Target
- Executive KPI cards

### Business Purpose

This page allows management to quickly understand overall business performance before drilling into specific products, regions, customers, or operational metrics.

---

## Page 2 — Product & Category Performance

![Product & Category Performance](PNG/Dashboard%202.PNG)

This page evaluates product-level and category-level performance.

### Key Analysis

- Sales by Category
- Profit by Category
- Product Performance Matrix
- Top 10 Products by Sales
- Product Sales vs Profitability
- Sales by Sub-Category

### Top Products by Sales

| Product | Approx. Sales |
|---|---:|
| Orbit 5G Smartphone | ₹86M |
| SoundMax Wireless Headphones | ₹61M |
| FastCharge Power Bank | ₹54M |
| Smartwatch Fit | ₹33M |
| Pulse Pro Smartphone | ₹17M |
| USB-C Hub | ₹15M |
| Nova X Smartphone | ₹7M |
| Echo Bluetooth Speaker | ₹4M |
| Moisturizer SPF 30 | ₹3M |
| Electric Kettle | ₹2M |

### Business Purpose

This page helps identify the products and categories responsible for revenue generation and profitability.

---

## Page 3 — Regional & Customer Performance

![Regional & Customer Performance](PNG/Dashboard%203.PNG)

This page evaluates business performance across geographic regions and customer segments.

### Regional Sales

| Region | Sales |
|---|---:|
| South | ₹72.72M |
| North | ₹71.58M |
| East | ₹70.07M |
| West | ₹49.11M |
| Central | ₹38.81M |

### Customer Segment Sales

| Customer Segment | Sales |
|---|---:|
| Consumer | ₹220.06M |
| Corporate | ₹48.39M |
| Small Business | ₹33.84M |

### Key Metrics

- Net Sales
- Net Profit
- Net Profit Margin
- Completed Orders
- Net AOV
- Regional Sales
- Regional Profit
- Customer Segment Sales
- Customer Segment Profitability

### Business Purpose

The page helps management compare geographic performance and understand which customer groups contribute most to revenue and profit.

---

## Page 4 — Order & Operations Performance

![Order & Operations Performance](PNG/Dashboard%204.PNG)

This page focuses on transaction quality and operational performance.

### Order Status

| Status | Orders | Share |
|---|---:|---:|
| Completed | 9,083 | 90.83% |
| Cancelled | 513 | 5.13% |
| Returned | 404 | 4.04% |
| **Total** | **10,000** | **100%** |

### Payment Performance

The dashboard compares sales generated through:

- UPI
- Credit Card
- Debit Card
- Net Banking
- Cash

UPI is the leading payment mode by sales value at approximately **₹113M**.

### Operational Analysis

- Order Status Distribution
- Monthly Order Volume
- Monthly Order Status Trend
- Cancelled Orders by Region
- Returned Orders by Category
- Payment Sales
- Completion Rate
- Cancellation Rate
- Return Rate

### Business Purpose

This page helps identify operational leakage and customer transaction behavior through cancellation, return, completion, and payment analysis.

---

## Page 5 — Management Performance & Targets

![Management Performance & Targets](PNG/Dashboard%205.PNG)

The final dashboard page focuses on management targets and performance gaps.

### Overall Target Performance

| Metric | Value |
|---|---:|
| Net Sales | ₹273.17M |
| Sales Target | ₹502.12M |
| Target Achievement | 60.20% |
| Target Variance | -₹199.83M |

### Regional Target Achievement

| Region | Target Achievement |
|---|---:|
| East | 89% |
| Central | 82% |
| North | 66% |
| South | 61% |
| West | 33% |

### Business Purpose

This page identifies where actual performance is falling short of management expectations and highlights regions requiring attention.

---

# Key Business Insights

## 1. Strong Overall Profitability

The business generated approximately **₹273.17M in net sales** and **₹67.55M in net profit**, producing a **24.73% net profit margin**.

This indicates that the business is generating substantial profit from completed transactions.

---

## 2. South Leads Regional Sales

South generated approximately **₹72.72M in sales**, making it the strongest region by sales value.

North and East followed closely with approximately **₹71.58M** and **₹70.07M** respectively.

Central recorded the lowest sales at approximately **₹38.81M**.

---

## 3. Electronics Dominates Revenue

Electronics generated approximately **₹279.98M** in total sales.

This represents approximately **92.6% of total sales**, making electronics the dominant revenue category.

This level of concentration creates both a strength and a potential business risk because overall revenue is highly dependent on one category.

---

## 4. Consumer Customers Drive Revenue

The Consumer segment generated approximately **₹220.06M** in sales.

This represents roughly **72.8% of total sales**, significantly exceeding Corporate and Small Business segments.

---

## 5. Strong Order Completion

Approximately **90.83% of orders were completed**.

However:

- **5.13%** were cancelled.
- **4.04%** were returned.

Together, these operational outcomes represent an area where the business can potentially reduce revenue leakage and improve customer experience.

---

## 6. UPI Is the Leading Payment Method

UPI generated approximately **₹113M in sales**, making it the leading payment method by sales value.

This indicates strong adoption of digital payment behavior within the analyzed transactions.

---

## 7. Target Achievement Requires Attention

Overall target achievement is approximately **60.20%**, with a target variance of approximately **-₹199.83M**.

This represents the most significant management-level performance gap identified in the analysis.

---

## 8. Significant Regional Target Variation

East achieved approximately **89%** of its target, while West achieved only approximately **33%**.

This large difference suggests that regional strategies may need to be differentiated rather than applying the same approach across all markets.

---

# Business Recommendations

### 1. Reduce Revenue Concentration Risk

Electronics contributes the overwhelming majority of sales.

Management should consider developing stronger sales strategies for other categories such as:

- Beauty & Personal Care
- Home & Kitchen
- Fashion
- Grocery

Diversification could reduce dependence on electronics.

### 2. Investigate West Region Performance

West has the weakest target achievement at approximately **33%**.

A deeper investigation should focus on:

- Product mix
- Customer acquisition
- Pricing
- Discounts
- Order cancellations
- Returns
- Regional demand
- Sales execution

### 3. Reduce Cancellation and Return Rates

The business records a **5.13% cancellation rate** and **4.04% return rate**.

Management can investigate the underlying reasons for these transactions and identify opportunities to improve order fulfillment and customer satisfaction.

### 4. Replicate High-Performing Regional Strategies

East demonstrates strong target achievement at approximately **89%**.

The practices contributing to East's performance can be reviewed and potentially adapted for weaker regions.

### 5. Strengthen Non-Electronics Categories

Because electronics dominates revenue, increasing the contribution of other categories can create a more balanced revenue portfolio.

### 6. Use Payment Insights for Customer Strategy

UPI is the leading payment method.

The business can use this insight when designing checkout experiences, promotional campaigns, and payment-related customer incentives.

---

# Dashboard Interactivity

The Power BI report provides interactive filtering capabilities.

Available filters include:

- Year
- Region
- Category
- Payment Mode

These filters allow management users to move from an overall business view into more specific performance segments.

---

# Design & Visualization

The dashboard visual design was developed with a focus on:

- Executive readability
- Consistent visual hierarchy
- KPI visibility
- Business-focused chart selection
- Clear comparison of actual vs target
- Consistent dashboard backgrounds
- Professional portfolio presentation

**Figma** was used for visual/design work and **GIMP** was used for supporting graphical assets.

---

# Tools & Technologies

| Tool | Purpose |
|---|---|
| Microsoft Excel | Data source and structured datasets |
| Power Query | Data cleaning and transformation |
| Microsoft Power BI | Dashboard development and BI reporting |
| DAX | KPI and analytical calculations |
| Figma | Dashboard visual/design assets |
| GIMP | Graphic editing and supporting visuals |
| GitHub | Project documentation and portfolio hosting |

---

# Skills Demonstrated

### Data Analytics

- Sales analysis
- Profitability analysis
- Customer segmentation
- Product performance analysis
- Regional analysis
- Operational analysis
- Target-performance analysis

### Excel

- Structured datasets
- Data organization
- Data validation
- Multi-table business data handling

### Power Query

- Data transformation
- Data preparation
- Data-type handling
- Data-quality validation

### Power BI

- Interactive dashboards
- KPI development
- Business reporting
- Data modeling
- Drill-down analysis
- Executive reporting

### DAX

- Measure development
- Sales calculations
- Profit calculations
- Ratio calculations
- Target analysis
- Performance metrics

### Business Intelligence

- KPI design
- Management reporting
- Performance monitoring
- Variance analysis
- Business recommendations

---

# Project Workflow

```text
Business Requirement
        |
        v
Dataset Understanding
        |
        v
Excel Data Preparation
        |
        v
Power Query Transformation
        |
        v
Power BI Data Model
        |
        v
DAX Measures
        |
        v
Dashboard Development
        |
        v
Business Analysis
        |
        v
Insights & Recommendations
        |
        v
GitHub Documentation
```

---

# Repository Structure

```text
retail-sales-performance-analysis/
│
├── Retail_Sales_Analysis_Day1.pbix
├── Retail_Sales_Analysis_Day1.xlsx
│
├── Background/
│   ├── 1.png
│   ├── 2.png
│   ├── 3.png
│   ├── 4.png
│   ├── 5.png
│   ├── 6.png
│   └── Color palette.png
│
├── PNG/
│   ├── Dashboard 1.PNG
│   ├── Dashboard 2.PNG
│   ├── Dashboard 3.PNG
│   ├── Dashboard 4.PNG
│   ├── Dashboard 5.PNG
│   └── Retail_Sales_Analysis_Day1.pdf
│
└── README.md
```

---

# Project Results

The completed Power BI solution provides a centralized analytical view of retail performance.

### Overall Performance

- **₹273.17M Net Sales**
- **₹67.55M Net Profit**
- **24.73% Net Profit Margin**
- **10K Orders**
- **23K Quantity**
- **90.83% Completion Rate**
- **5.13% Cancellation Rate**
- **4.04% Return Rate**
- **60.20% Target Achievement**

### Major Business Findings

- South is the strongest region by sales.
- Electronics dominates total revenue.
- Consumer customers generate the majority of sales.
- UPI is the leading payment method.
- Order completion is strong but cancellation and return activity remains relevant.
- Overall target achievement is significantly below the assigned target.
- West has the largest regional target-performance gap.

---

# Limitations

The analysis has several limitations:

- The underlying source is confidential and cannot be publicly disclosed.
- The project focuses on the fields available in the provided dataset.
- No external market or competitor data was incorporated.
- Marketing campaign effectiveness is outside the scope of this dashboard.
- Customer lifetime value is not included.
- Inventory and supply-chain performance are not included.
- The analysis is dependent on the quality and completeness of the available business data.

---

# Future Improvements

Future versions of the project could include:

- Customer lifetime value analysis
- Inventory and stock-level analytics
- Product demand forecasting
- Sales forecasting
- Customer churn analysis
- Marketing campaign ROI
- Discount effectiveness analysis
- Regional sales forecasting
- Automated Power BI refresh
- Advanced statistical analysis
- Predictive analytics
- Drill-through customer and product profiles

---

# Project Type

**Personal Portfolio Project**

### Duration

**3 Days**

### Role

**Data Analyst**

### Primary Focus

**Retail Business Intelligence & Sales Performance Analytics**

---

# AI Assistance

AI tools were used as supporting resources during the development and documentation process.

**AI Assistance:** ChatGPT

AI assistance was used for areas such as:

- Analytical planning
- DAX development support
- Documentation structure
- Business-insight interpretation
- README development
- Technical problem-solving support

The final dashboard, data preparation, analysis, visualization decisions, and project implementation were developed as part of the project workflow.

---

# Author

## Altamash Nizamuddin

**Data Analyst | Power BI • Python • MySQL**

Focused on transforming business data into actionable insights through analytics, visualization, and Business Intelligence.

### GitHub

[![GitHub](https://img.shields.io/badge/GitHub-altamash--analyst-black?logo=github)](https://github.com/altamash-analyst)

- **LinkedIn:** [Altamash Nizamuddin](https://www.linkedin.com/in/altamash-nizamuddin-a208152a3/)
- **GitHub:** [altamash-analyst](https://github.com/altamash-analyst)
- **Email:** [altamash9876@gmail.com](mailto:altamash9876@gmail.com)

**Location:** Mumbai, India

### Target Roles

- Data Analyst
- Business Analyst
- BI Analyst
- Power BI Developer

### Work Preference

**Remote**

---

# Keywords

`Retail Sales Analysis`  
`Retail Analytics`  
`Sales Performance Analysis`  
`Power BI Dashboard`  
`Power BI Project`  
`Power BI DAX`  
`DAX Analytics`  
`Power Query`  
`Excel Analytics`  
`Business Intelligence`  
`Data Analyst Portfolio`  
`Business Analyst Portfolio`  
`Sales Dashboard`  
`Retail Business Intelligence`  
`Data Visualization`  
`KPI Dashboard`  
`Target Analysis`  
`Profitability Analysis`  
`Altamash-Analyst`

---

# Conclusion

The Retail Sales Performance Analysis project demonstrates how structured business data can be transformed into an interactive Business Intelligence solution using Excel, Power Query, Power BI, and DAX.

The dashboard provides management with visibility into sales performance, profitability, product contribution, regional performance, customer segments, order operations, payment behavior, and target achievement.

The analysis identifies clear business strengths, including strong profitability, high order completion, strong performance in leading regions, and significant demand for electronics. At the same time, it highlights important management concerns such as revenue concentration, cancellation and return activity, and substantial target underperformance.

The project demonstrates an end-to-end analytical workflow from **data preparation to business insight and management reporting**.
