# 📦 E-Commerce Sales Analytics Data Pipeline
**Databricks | Delta Lake | Medallion Architecture**

---

## 📌 Project Overview
This project implements an **end-to-end E-Commerce data analytics pipeline** using **Databricks** and **Delta Lake**, following the **Medallion Architecture (Bronze → Silver → Gold)**.

In addition to the standard pipeline, it also includes:
- Data quality validation and governance
- Quarantine handling for invalid records
- Incremental processing logic
- Analytics-ready Gold views
- Business-focused dashboards for validation and insights

> 🎯 **Goal:** Demonstrate real-world **Data Engineering best practices**, not just analytics.

---

## 🧱 Architecture Overview
```text
Source
  ↓
Bronze (Raw Delta)
  ↓
Silver (Cleansed Data)
  ↓
Silver – Data Quality Validation
  ↓
Silver – Quarantine / Rejected Records
  ↓
Gold (Facts, Dimensions, Views)
  ↓
Dashboards
```
**Architecture Overview:**  
This pipeline follows the **Databricks Medallion Architecture** (Bronze → Silver → Gold) and is extended with additional Silver-layer **data quality validation and quarantine handling** to reflect real-world data governance practices.

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

---

## 📊 Dashboards

### 1️⃣ Core Medallion Analytics Dashboard
**Purpose:**  
Validate the original Medallion pipeline and Gold modeling.

**Pic**
![E-Commerce Medallion Pipeline - Core Analytics](dashboards/E-Commerce%20Medallion%20Pipeline%20-%20Core%20Analytics.png)

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

**Pic**
![E-Commerce Data Quality & Analytics Validation Dashboard](dashboards/E-Commerce%20Data%20Quality%20&%20Analytics%20Validation%20Dashboard.png)

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
