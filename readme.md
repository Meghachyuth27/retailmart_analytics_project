# RetailMart Analytics Platform

**End-to-End Retail Analytics System** (Data Warehouse → KPIs → JSON APIs → Interactive Dashboard)

---

## Overview

RetailMart Analytics is a full-stack analytics platform designed to process retail business data and deliver actionable insights.

**It includes:**

- PostgreSQL analytics schema
- KPI metadata and audit logging
- Complete Customer, Product, Sales, and Store analytics modules
- Optimized materialized views and real-time views
- A fully interactive web dashboard (HTML + CSS + JS + Chart.js)
- Modular JSON data layer powering all dashboard visuals

---

## 1. Database Setup

### Create Analytics Schema

Creates a dedicated analytics workspace and grants read-access.

**Source:** `create_analytics_schema`

### Create Metadata & Audit Tables

Tracks KPIs, refresh schedules, data lineage, and SQL execution logs.

**Source:** `create_metadata_tables`

**Tables included:**

- `analytics.kpi_metadata`
- `analytics.audit_log`
- `analytics.log_operation()` function

---

## 2. KPI Modules

### Customer Analytics

**Source:** `customer_analytics`

**Features:**

- Customer Lifetime Value (CLV)
- RFM segmentation (Recency, Frequency, Monetary)
- Cohort retention
- Churn risk classification
- Loyalty analysis
- Customer status tagging
- Indexing for fast BI workloads

**Materialized views:**

- `mv_customer_lifetime_value`
- `mv_rfm_analysis`
- `mv_cohort_retention`

### Product Analytics

**Source:** `product_analytics`

**Features:**

- Top product performance (units, revenue)
- Category-level statistics
- Brand-level market share
- ABC Pareto classification (80/20)
- Inventory coverage and valuation
- Ranking within category and overall

**Outputs:**

- `mv_top_products`
- `vw_category_performance`
- `vw_brand_performance`

### Sales Analytics

**Source:** `sales_analytics`

**Features:**

- Daily, monthly, quarterly sales views
- Moving averages (3-month, 6-month)
- MoM & YoY growth calculations
- Day-of-week analysis
- Payment mode analysis
- Returns analysis
- Executive KPI summaries

**Views & materialized views:**

- `vw_daily_sales_summary`
- `mv_monthly_sales_dashboard`
- `vw_recent_sales_trend`
- `vw_sales_by_dayofweek`
- `vw_sales_by_payment_mode`

### Store Analytics

**Source:** `store_analytics`

**Features:**

- Store-level profitability
- Regional rollups
- Employee productivity
- Inventory health scoring
- Revenue & profit ranking
- Global refresh function

**Outputs:**

- `mv_store_performance`
- `vw_regional_performance`
- `vw_store_inventory_status`
- `vw_employee_by_store`

---

## 3. Dashboard Implementation

### Dashboard JavaScript Controller

**Source:** `dashboard`

**Responsibilities:**

- Loads all JSON datasets
- Caches data for performance
- Renders charts using Chart.js
- Updates KPI cards and tables
- Handles responsive resizing
- Includes internal debugging and logging

### HTML Dashboard Structure

**Source:** `index`

**Includes:**

- Navigation tabs
- KPI cards
- Trend charts
- Category charts
- Tables for products, customers, stores
- Fully responsive grid layout

### Dashboard Styling (CSS)

**Source:** `styles`

**Features:**

- Modern UI theme
- Gradient header
- Sticky navigation
- KPI card hover effects
- Responsive chart/tables layout
- Clean typography and spacing

---

## 4. Folder Structure

```
/
├── 01_setup/
│   ├── create_analytics_schema.sql
│   └── create_metadata_tables.sql
├── 02_kpi_queries/
│   ├── customer_analytics.sql
│   ├── product_analytics.sql
│   ├── sales_analytics.sql
│   └── store_analytics.sql
├── 03_dashboard/
│   └── dashboard.js
├── 05_dashboard/
│   ├── index.html
│   └── styles.css
└── data/
    ├── sales/
    ├── products/
    ├── customers/
    └── stores/
```

---

## 5. How to Run the Project

### Step 1: Initialize the Database

Run scripts in this order:

1. `01_setup/create_analytics_schema.sql`
2. `01_setup/create_metadata_tables.sql`
3. `02_kpi_queries/customer_analytics.sql`
4. `02_kpi_queries/product_analytics.sql`
5. `02_kpi_queries/sales_analytics.sql`
6. `02_kpi_queries/store_analytics.sql`

### Step 2: Generate JSON Data

Export view/materialized view results to:

- `/data/sales/`
- `/data/products/`
- `/data/customers/`
- `/data/stores/`

Ensure filenames match those requested in `dashboard.js`.

### Step 3: Launch the Dashboard

Any static server works. Example:

```bash
python3 -m http.server 8000
```

Open: `http://localhost:8000/index.html`

---

## 6. Key Features Summary

| Area | Capabilities |
|------|-------------|
| Schema | Dedicated analytics workspace |
| Governance | KPI metadata + audit logging |
| Customer Analytics | CLV, RFM, cohort, churn |
| Product Analytics | ABC, category, brand, inventory |
| Sales Analytics | MoM/YoY, trends, payment modes |
| Store Analytics | Profitability, region, employees |
| Dashboard | KPIs, charts, tables, interactivity |

---

## 7. Suggested Enhancements

- Automate MV refresh with Airflow/Cron
- Convert JSON exports into REST APIs
- Add ML forecasting (Prophet, XGBoost)
- Add role-based access control for dashboard
- Implement anomaly detection alerts