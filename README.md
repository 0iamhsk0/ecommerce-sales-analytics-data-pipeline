# 📦 E-Commerce Sales Analytics Data Pipeline
**Databricks | Delta Lake | Medallion Architecture**

---

## 📌 Project Overview
This project implements an **end-to-end E-Commerce data analytics pipeline** using **Databricks** and **Delta Lake**, following the **Medallion Architecture (Bronze → Silver → Gold)**.

In addition to the standard pipeline, the project includes:
- Data quality validation and governance
- Quarantine handling for invalid records
- Incremental processing logic (job-ready design)
- Analytics-ready Gold views
- Business-focused dashboards for validation and insights

> 🎯 **Goal:** Demonstrate real-world **Data Engineering best practices**, not just analytics.

---

## 🧱 Architecture Overview

```text
Source Data
   ↓
Bronze Layer (Raw Ingestion)
   ↓
Silver Layer (Cleaned + Validated)
   ↓
Gold Layer (Analytics & Business Views)
   ↓
Dashboards (Insights & Validation)
```

---

## 🥉 Bronze Layer – Raw Ingestion
- Stores raw e-commerce data in **Delta format**
- No transformations applied
- Preserves original schema and values
- Acts as a recovery and audit layer

---

## 🥈 Silver Layer – Cleansing & Data Quality
The Silver layer prepares data for analytics and governance.

### ✔ Key Features
- Schema standardization  
- Null and value validation  
- Referential integrity checks  
- Duplicate detection  

### 🔍 Data Quality Checks
Implemented using **Spark SQL notebooks**:
- `invalid_customers`
- `duplicate_customers`
- `invalid_products`
- `invalid_order_items`

📁 **Location:**  
`/data_quality`

### 🚧 Quarantine Handling
Invalid records are isolated into **quarantine tables** with rejection reasons:
- Prevents bad data from entering Gold
- Enables traceability and auditability
- Mirrors real-world data governance workflows

---

## 🥇 Gold Layer – Analytics & Business Modeling

### 📊 Core Gold Tables
- `gld_fact_order_items`
- `gld_dim_customers`
- `gld_dim_products`
- `gld_dim_date`
- `fact_transactions_denorm` *(denormalized analytics table)*

📁 **Location:**
- Dimensions → `/medallion_processing_dim`
- Facts → `/medallion_processing_fact`

### 📈 Analytics Views (Gold)
Instead of duplicating tables, **analytics views** are created on top of Gold facts:
- Daily sales performance
- Customer lifetime value
- Channel-wise performance
- Coupon / discount impact analysis

✔ Improves maintainability  
✔ Reduces storage overhead  
✔ Follows analytics engineering best practices  

---

## 🔁 Incremental Processing Design
Although the dataset is static, the pipeline is designed to be **incremental-ready**:
- Metadata-based watermark logic
- Idempotent transformations
- Re-runnable notebooks without duplication

📌 **Design decision:**  
Jobs and scheduled pipelines were intentionally not created, as the dataset does not change.  
The pipeline is **job-ready** and can be scheduled if real-time or periodic data sources are introduced.

---

## 📊 Dashboards

### 1️⃣ Core Medallion Analytics Dashboard
**Purpose:**  
Validate the original Medallion pipeline and Gold modeling.

**Key Insights:**
- Monthly sales trend
- Revenue by category
- Time-based sales patterns

📁 **Assets:**  
`/dashboards`

---

### 2️⃣ Data Quality & Analytics Validation Dashboard
**Purpose:**  
Demonstrate how data quality and governance improve business analytics.

**Includes:**
- KPI cards (Total Revenue, Total Transactions, Avg Transaction Value)
- Revenue trends
- Channel-wise revenue
- Top customers by lifetime value
- Coupon vs non-coupon revenue comparison

This dashboard directly links **data engineering decisions → business impact**.

---

## 🗂️ Project Structure

```text
ecommerce-sales-analytics-data-pipeline/
├── setup/                     # Initial setup & configurations
├── medallion_processing_dim/  # Dimension table processing
├── medallion_processing_fact/ # Fact table processing
├── data_quality/              # Validation & quarantine logic
├── dashboards/                # Dashboard-related assets
├── README.md
```
---

## 🛠️ Technologies Used
- Databricks  
- Apache Spark  
- Delta Lake  
- Databricks SQL Dashboards  
- GitHub (Databricks Repos integration)

---

## 🎯 Key Learnings & Outcomes
- Implemented a complete **Medallion Architecture**
- Applied **data quality & governance** patterns
- Designed **analytics-ready Gold views**
- Built **business-facing dashboards**
- Practiced **incremental & job-ready pipeline design**

---

## 📌 Disclaimer
This project uses a **static dataset** for learning and portfolio purposes.  
Pipeline orchestration and scheduling were intentionally omitted to reflect **realistic engineering decisions**.



