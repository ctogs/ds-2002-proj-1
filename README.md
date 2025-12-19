# Data Project 2 (Capstone) — Local PySpark Dimensional Lakehouse

## Business Process

I modeled **retail sales transactions** as the business process, capturing the interaction between customers, products, and time. The Project 2 notebook is located in `project2.ipynb`.

This implementation is a **local PySpark equivalent** of the “Databricks lakehouse” requirements (Bronze → Silver → Gold) using Spark’s batch and Structured Streaming APIs—**no Azure/Databricks required**.

## Dimensional Lakehouse Design (Bronze → Silver → Gold)

### Gold Dimension Tables
- **dim_date**: Date dimension for temporal analysis (sourced from local CSV)
- **dim_customer**: Customer reference data (sourced from MySQL)
- **dim_product**: Product reference data (sourced from MySQL)
- **dim_category**: Product category dimension (derived from product attributes)

### Gold Fact Tables
- **fact_sales**: Sales transaction fact table (conformed from streaming ingestion)
- **fact_sales_margin**: Enriched metric table (gross margin) computed by joining sales with MongoDB product costs

## Required Source Systems (All Demonstrated)

This project integrates data from **three required source types**:

1. **MySQL (Relational / SQL)**  
   - Source tables: `src_customers`, `src_products`  
   - Access method: Spark **JDBC** read/write

2. **MongoDB (NoSQL)**  
   - Collection: `product_costs`  
   - Access method: `pymongo`

3. **Local File System (Files)**  
   - CSV inputs in `data/`: `dates.csv`, `sales.csv` (and additional CSVs retained from Project 1)  
   - Streaming inputs: JSON drops written into `project2_stream/incoming/`

## Data Integration & Processing Requirements

### 1) Batch Execution + Incremental Load (Local Equivalent)
- **Batch execution**: A baseline batch load populates lakehouse tables.
- **Incremental load (batch)**: The notebook appends a small incremental batch and shows the Bronze row counts increasing.

### 2) Near Real-Time Streaming (Mini-batches) + Bronze/Silver/Gold
- **3 streaming intervals**: The fact data is segmented into **3 separate JSON files** and ingested as **Structured Streaming mini-batches** (local equivalent of “AutoLoader” behavior).
- **Silver integration**: Streaming fact rows are joined to static reference dimensions (customer/product) at the **Silver** stage to illustrate the relationships between near real-time and static data.
- **Gold publishing**: Conformed facts and dimensions are published for analytics queries.

### 3) Business Value / Analytics
The notebook includes analytical queries that aggregate revenue and gross margin by time, category, and customer using the Gold star schema tables.

## Output Artifacts

The notebook writes local lakehouse outputs to:
- `project2_lakehouse/bronze/`
- `project2_lakehouse/silver/`
- `project2_lakehouse/gold/`

Streaming artifacts:
- Incoming streaming drops: `project2_stream/incoming/`
- Streaming checkpoints: `project2_stream/checkpoints/`

These generated outputs are ignored by git via `.gitignore` so the repository remains clean and reproducible.


