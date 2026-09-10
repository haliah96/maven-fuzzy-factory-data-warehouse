# Maven Fuzzy Factory — Data Warehouse & Data Mart

Data Warehouse and Data Mart implementation using Pentaho Data Integration (PDI) and PostgreSQL.

## Project Overview

This project implements an end-to-end data pipeline for Maven Fuzzy Factory, covering data movement and transformation from raw data to analytical data marts.

The pipeline follows this architecture:

**Raw → Staging → Data Warehouse → Data Mart**

The Data Warehouse is designed using a **Star Schema** with 4 dimension tables and 2 fact tables. Three aggregated data marts are then created and prepared for Tableau visualization.

## Tools

- Pentaho Data Integration (PDI)
- PostgreSQL
- DBeaver

## Data Warehouse Architecture

The Data Warehouse uses a Star Schema consisting of:

### Dimension Tables

- `dim_campaign`
- `dim_date`
- `dim_device`
- `dim_product`

### Fact Tables

- `fact_order`
- `fact_pageviews`

The fact tables are connected to the dimension tables using surrogate keys and dimension lookups.

## ETL Pipeline

### 1. Staging ETL

The staging process moves data from the raw schema into the staging schema using Pentaho transformations and jobs.

The process includes:

- Parameterized ETL using `${table_name}`
- Data movement from Raw → Staging
- Logging
- Job orchestration

### 2. Data Warehouse ETL

Data is transformed from the staging layer into dimension and fact tables.

Pentaho transformations use:

- Table Input
- Select Values
- CASE WHEN / conditional logic
- Dimension Lookup/Update
- Database Lookup
- Calculator
- Surrogate keys
- NULL handling

The `profit_usd` metric is calculated as:

`profit_usd = price_usd - cogs_usd`

### 3. Data Mart

Three aggregated data marts are created for analytical purposes:

- `dm_ecommerce_sales`
- `dm_marketing_campaign`
- `dm_page_view`

The data marts are aggregated and prepared for Tableau visualization.

## Data Mart Use Cases

### E-commerce Sales

Supports analysis of sales trends and transaction performance.

### Marketing Campaign

Supports analysis of marketing campaign effectiveness and sales performance.

### Website Traffic

Supports analysis of page views and website visitor behavior for funnel optimization.

## Repository Structure

```text
.
├── dimensions/
│   ├── dim_campaign.ktr
│   ├── dim_date.ktr
│   ├── dim_device.ktr
│   └── dim_product.ktr
│
├── facts/
│   ├── fact_order.ktr
│   └── fact_pageviews.ktr
│
├── data_marts/
│   ├── dm_ecommerce_sales.ktr
│   ├── dm_marketing_campaign.ktr
│   └── dm_page_view.ktr
│
├── jobs/
│   └── dwh_maven_job.kjb
│
└── README.md
```

## Skills Demonstrated

### Data Engineering / ETL

- Pentaho Data Integration
- ETL pipeline development
- Transformation (`.ktr`)
- Job orchestration (`.kjb`)
- Parameterized ETL
- Logging
- Source-to-target validation
- NULL handling
- Surrogate keys
- Dimension lookup

### Database & Analytics

- PostgreSQL
- SQL
- Star Schema
- Fact and Dimension modeling
- Revenue, cost, profit, order, and pageview metrics
- Data Mart preparation for Tableau

## Project Outcome

The project produces a Data Warehouse with **4 dimension tables and 2 fact tables**, followed by **3 analytical data marts** for sales, marketing campaign, and website traffic analysis.

The implementation demonstrates an end-to-end data workflow using Pentaho, from data ingestion and logging through transformation, star schema modeling, and preparation of analytical data marts.
