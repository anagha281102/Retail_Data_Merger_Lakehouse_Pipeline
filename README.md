# 🛒 FMCG Data Consolidation: End-to-End Data Engineering Project

## 📖 Project Overview
In the fast-paced **FMCG (Fast-Moving Consumer Goods)** sector, mergers and acquisitions are common. This project simulates a real-world scenario where a large retail giant acquires a smaller company. 

The objective was to design and implement a scalable **ETL Pipeline** to consolidate disparate data sources into a single, unified **Databricks Lakehouse**. By leveraging a Medallion Architecture, we ensure that the business receives high-quality, actionable insights from the newly merged data.

---

## 🏗 System Architecture
The data flows through three distinct layers to ensure reliability and performance:



1.  **🥉 Bronze (Raw):** Ingests raw CSV files from the **Amazon S3 Data Lake**. It stores data in its native format while adding audit metadata (source file name, ingestion time).
2.  **🥈 Silver (Cleaned):** Data is refined, schema enforcement is applied, and duplicates are removed. This layer provides a "Single Source of Truth."
3.  **🥇 Gold (Curated):** Business-level aggregates, specialized dimension tables (like `dim_date`), and fact tables optimized for high-speed BI reporting.

---

## 🛠 Tech Stack & Tools
* **Data Lake:** Amazon S3 (Scalable object storage for raw and processed files).
* **Processing Engine:** Apache Spark (PySpark) & SQL.
* **Storage Format:** Delta Lake (Enables ACID transactions and Time Travel).
* **Orchestration:** Databricks Notebooks & Workflows.
* **AI & Analytics:** * **Databricks Genie:** An AI-powered natural language interface for data querying.
    * **SQL Dashboards:** Built-in Databricks visualizations for executive reporting.

---

## 📂 Repository Structure
| File | Description |
| :--- | :--- |
| `setup_catalog.ipynb` | Initializes Unity Catalog, `fmcg` catalog, and schemas. |
| `utilities.ipynb` | Shared helper functions and global configuration variables. |
| `1_customers_data_processing.ipynb` | ETL for customer master records. |
| `2_products_data_processing.ipynb` | ETL for product catalog and inventory. |
| `3_pricing_data_processing.ipynb` | Pricing logic using Window functions and ranking. |
| `1_full_load_fact.ipynb` | Historical "Big Bang" load of the sales fact table. |
| `2_incremental_load_fact.ipynb` | Daily CDC (Change Data Capture) using Delta `MERGE`. |
| `dim_date_table_creation.ipynb` | Standardized calendar dimension for time-intelligence. |

---

## ✨ Key Features
* **🚀 Efficient Ingestion:** Decoupled storage and compute by using Amazon S3 as the primary Data Lake.
* **🤖 AI-Powered Insights:** Integrated **Databricks Genie**, allowing non-technical stakeholders to ask questions like *"What were the sales in Q3?"* in plain English.
* **📊 Executive Dashboard:** Created a comprehensive BI Dashboard in Databricks to track KPIs, sales trends, and integration progress.
* **🔧 Dynamic Pipelines:** Used Databricks Widgets for parameterization, making the code reusable across different environments.
* **📈 Incremental Loading:** Optimized costs by only processing new or changed records rather than the entire dataset.

---

## ⚙️ Setup Instructions
1.  **Environment:** Provision a Databricks Community Edition or Standard workspace.
2.  **Data Lake:** Upload your raw FMCG data (Customers, Products, Orders) to an **Amazon S3** bucket.
3.  **Authentication:** Configure S3 Mount points or use IAM roles for Databricks access.
4.  **Bootstrap:** Run `setup_catalog.ipynb` to create the database structure.
5.  **Execution:** Run the notebooks in numerical order to populate the Lakehouse.
6.  **Visualization:** Navigate to the SQL side of Databricks to view the pre-built Dashboards and interact with Genie.
