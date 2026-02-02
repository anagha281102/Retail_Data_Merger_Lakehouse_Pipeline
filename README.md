# FMCG Data Consolidation: End-to-End Data Engineering Project

## 📌 Project Overview
This project demonstrates a real-world data engineering use case in the **FMCG (Fast-Moving Consumer Goods)** domain. The scenario simulates a large retail company acquiring a smaller competitor. The goal is to build a robust, end-to-end ETL pipeline that consolidates data from both entities into a unified **Databricks Lakehouse** environment.



## 🛠 Tech Stack
* **Language:** Python (PySpark), SQL
* **Platform:** Databricks (Community Edition)
* **Data Lake:** Amazon S3 (Primary storage for raw landing and Delta files)
* **Data Format:** Delta Lake (ACID transactions, Time Travel, Schema Evolution)
* **Architecture:** Medallion Architecture (Bronze, Silver, Gold)
* **AI Integration:** Databricks Genie (Natural Language to SQL)
* **Visualization:** Databricks SQL Dashboards

## 🏗 Project Architecture
The pipeline follows the industry-standard **Medallion Architecture** to ensure data reliability and high quality:

1.  **Bronze (Raw):** Ingests raw CSV data from the **Amazon S3 Data Lake**. It preserves the original state of data while adding audit metadata (file names, ingestion timestamps).
2.  **Silver (Cleaned):** Transforms raw data by performing cleaning, deduplication, and strict schema enforcement.
3.  **Gold (Curated):** Creates business-level aggregates, dimension tables (e.g., `dim_date`), and fact tables optimized for analytics and BI.

## 📂 Repository Structure
* `setup_catalog.ipynb`: Initializes the Unity Catalog, creates the `fmcg` catalog, and establishes the `bronze`, `silver`, and `gold` schemas.
* `utilities.ipynb`: Centralized notebook for shared variables and helper configurations.
* `1_customers_data_processing.ipynb`: ETL pipeline for customer master data.
* `2_products_data_processing.ipynb`: ETL pipeline for product catalog information.
* `3_pricing_data_processing.ipynb`: Processes pricing data using window functions for ranking and deduplication.
* `1_full_load_fact.ipynb`: Handles the initial historical load of the sales/orders fact table.
* `2_incremental_load_fact.ipynb`: Manages daily incremental updates using Delta Lake’s `MERGE` capability.
* `dim_date_table_creation.ipynb`: Generates a calendar dimension table for time-series analysis.

## 🚀 Key Features
* **Amazon S3 Data Lake:** Scalable ingestion reading directly from S3 buckets using PySpark.
* **Incremental Loading:** Efficiently updates fact tables to save compute costs.
* **Databricks Genie:** Integrated AI Space that allows users to query the consolidated data using natural language.
* **BI Dashboard:** A built-in Databricks SQL Dashboard providing visual insights into consolidated sales and inventory metrics.
* **Parameterization:** Dynamic execution using Databricks Widgets for flexibility across different catalogs or sources.

## 📋 Setup Instructions
1.  **Databricks Environment:** Set up a Databricks Community Edition account.
2.  **S3 Configuration:** Upload the raw CSV files (Customers, Products, Pricing, Orders) to your Amazon S3 bucket and configure access via Databricks.
3.  **Catalog Setup:** Execute `setup_catalog.ipynb` first to build the database infrastructure.
4.  **Run Pipelines:** Execute the processing notebooks in sequential order (1, 2, 3) to move data from Bronze to Gold.
5.  **Analytics:** Open the **Databricks SQL Dashboard** or use **Databricks Genie** to interact with the final Gold layer data.

---
*Note: This project serves as a comprehensive template for handling Data Engineering challenges during corporate Mergers and Acquisitions (M&A).*