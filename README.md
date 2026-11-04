# SQL Data Warehouse & ETL Pipeline

### End-to-End Data Engineering Project | SQL Server | Medallion Architecture | Business Analytics

## 1. Project Overview

This project implements an end-to-end Data Warehouse using Microsoft SQL Server and a Medallion Architecture (Bronze, Silver, Gold).

The objective is to integrate sales data from CRM and ERP systems, build automated ETL pipelines, improve data quality, and create an analytical data model for business intelligence and reporting.

### Key Features

- Multi-source data integration from CRM and ERP systems
- Automated ETL pipelines using T-SQL Stored Procedures
- Data cleaning, validation, and standardization
- Data quality checks and error handling
- Dimensional Data Modeling using a Star Schema
- Business analytics and KPI reporting

## 2. Data Architecture

The Data Warehouse follows a three-layer Medallion Architecture.

**CRM & ERP Sources → Bronze → Silver → Gold → Business Intelligence**

### Bronze Layer – Raw Data

- Ingests six CSV files from CRM and ERP systems
- Stores source data with minimal transformations
- Uses SQL Server `BULK INSERT`
- Automates ingestion with `bronze.load_bronze`

### Silver Layer – Cleaned Data

- Removes duplicate customer records
- Standardizes customer and product information
- Handles missing and invalid values
- Converts and validates dates
- Corrects sales and pricing inconsistencies
- Automates transformations with `silver.load_silver`

### Gold Layer – Business-Ready Data

Implements a dimensional Star Schema using SQL Views.

| View | Description |
|---|---|
| `gold.dim_customers` | Customer profiles, demographics, and geographic information |
| `gold.dim_products` | Product details, categories, and costs |
| `gold.fact_sales` | Sales transactions, quantities, prices, and dimension keys |

## 3. Technology Stack

| Technology | Purpose |
|---|---|
| SQL Server | Data Warehouse storage and processing |
| T-SQL | ETL development and data transformations |
| SSMS | Database development and administration |
| Stored Procedures | ETL automation |
| Window Functions | Deduplication and historical transformations |
| Star Schema | Dimensional Data Modeling |
| Git & GitHub | Version control and documentation |
| Power BI Desktop | Planned interactive dashboard |

## 4. Project Structure

```text
sql-data-warehouse-project/
|
|-- 00_setup/
|-- 01_datasets/
|   |-- source_crm/
|   |-- source_erp/
|
|-- 02_docs/
|
|-- 03_scripts/
|   |-- init_database.sql
|   |-- bronze/
|   |   |-- ddl_bronze.sql
|   |   |-- proc_load_bronze.sql
|   |-- silver/
|   |   |-- ddl_silver.sql
|   |   |-- proc_load_silver.sql
|   |-- gold/
|       |-- ddl_gold.sql
|
|-- 04_tests/
|-- LICENSE
|-- README.md
```

## 5. ETL Pipeline

The project provides two main stored procedures to automate data processing.

**Step 1 – Load Bronze**

```sql
EXEC bronze.load_bronze;
```

Loads raw CRM and ERP datasets into Bronze tables.

**Step 2 – Load Silver**

```sql
EXEC silver.load_silver;
```

Applies data cleaning, validation, standardization, and transformation rules.

**Step 3 – Build Gold**

Execute `03_scripts/gold/ddl_gold.sql` to create the analytical dimensions and fact view.

## 6. Data Quality

The project includes checks for:

- Duplicate customer identifiers
- Missing and invalid values
- Invalid dates
- Sales and pricing consistency
- Customer and product relationship integrity
- Standardized country, gender, and product attributes

The implemented validation queries returned zero duplicate customers, zero sales inconsistencies, and zero unmatched customer or product keys in the tested Gold dataset.

## 7. Business Analytics Results

The following KPIs were calculated from the Gold Layer.

| KPI | Result |
|---|---:|
| Total Revenue | 29,356,250 |
| Total Orders | 27,659 |
| Total Quantity Sold | 60,423 |
| Customers with Sales | 18,484 |
| Products Sold | 130 |
| Sales Records | 60,398 |

### Sales Performance Analysis

**Top-Selling Products**

- Water Bottle – 30 oz.: 4,249 units
- Patch Kit/8 Patches: 3,191 units
- Mountain Tire Tube: 3,096 units

**Top Markets by Revenue**

- United States: 9,162,327
- Australia: 9,060,172
- United Kingdom: 3,391,376

**Monthly Sales Trends**

The dataset covers transactions from December 2010 through January 2014. December 2013 recorded the highest monthly revenue observed in the 2013 analysis, reaching 1,874,128.

## 8. How to Run the Project

1. Install Microsoft SQL Server and SQL Server Management Studio.
2. Clone the repository.
3. Execute `03_scripts/init_database.sql` to create the database and schemas.
4. Execute the Bronze and Silver DDL scripts.
5. Update the CSV file paths in `proc_load_bronze.sql` for the local environment.
6. Execute the Bronze loading procedure.
7. Execute the Silver transformation procedure.
8. Execute `ddl_gold.sql` to create the analytical views.
9. Run the data quality validation scripts.
10. Explore the Gold Layer using SQL analytics.

## 9. Future Improvements

- Build an interactive Power BI dashboard
- Implement incremental data loading
- Improve ETL execution logging and monitoring
- Introduce automated data quality testing
- Add pipeline scheduling and orchestration

## 10. License

This repository retains the original MIT License and copyright notice applicable to the reused source material. See the `LICENSE` file for details.


## Power BI Sales Dashboard

An interactive sales performance dashboard built with
Power BI and SQL Server.

### Key Features
- Revenue, Orders, Customers, Products, and Quantity KPIs
- Top 8 Best-Selling Products
- Sales Revenue by Country
- Monthly Sales Trend

### Dashboard Preview

![Sales Performance Dashboard](05_dashboard/dashboard_preview.png)
