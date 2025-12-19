# ETL Data Processor - Retail Sales Data Mart

## Business Process

I chose **retail sales transactions** as my business process, modeling the interaction between customers, products, and sales over time. The project file is located in project1.ipynb.

## Data Mart Design

### Dimension Tables
- **DimCustomer**: Customer demographics and contact information
- **DimProduct**: Product catalog with categories and pricing
- **DimDate**: Temporal dimension for time-based analysis

### Fact Tables
- **FactSales**: Core sales transaction data
- **FactSales_Margin**: Enriched fact table with calculated gross margins

## Data Sources Integration

I successfully integrated data from **three different source systems**:

1. **MySQL OLTP Database**: Source customer and product tables (`src_customers`, `src_products`)
2. **CSV Files**: Local file system containing customers, products, dates, and sales data
3. **MongoDB**: NoSQL database storing product cost information (`product_costs`)

## ETL Pipeline Implementation

### Extract Phase
- **SQL Database**: Extracted customer and product data from MySQL OLTP tables
- **File System**: Loaded CSV files containing transactional and dimensional data
- **MongoDB**: Retrieved product cost data from NoSQL collection

### Transform Phase
- **Data Integration**: Combined data from multiple sources, handling duplicates
- **Column Modification**: Renamed and restructured columns for dimensional model
- **Business Logic**: Calculated gross margins by joining sales data with cost information
- **Data Quality**: Implemented deduplication and data validation

### Load Phase
- **Dimension Loading**: Populated customer, product, and date dimensions
- **Fact Loading**: Created sales fact table with proper foreign key relationships
- **Enriched Facts**: Generated margin analysis table with calculated metrics

## Analytical Queries

I developed six comprehensive analytical queries that demonstrate:

1. **Daily Revenue & Margin Analysis**: Time-series analysis of sales performance
2. **Category Performance**: Product category analysis by date
3. **Customer Segmentation**: Top customers by margin contribution
4. **Temporal Patterns**: Average order value by weekday
5. **Product Performance**: Product leaderboard by units, revenue, and margin
6. **Monthly Rollups**: Aggregated metrics by year/month

Each query joins 3+ tables and includes aggregation functions (SUM, COUNT, AVG) with GROUP BY operations.

## Deployment Strategy

The solution is designed for **local development and testing**:

1. **Database Setup**: MySQL database with configured connection parameters
2. **MongoDB Setup**: Local MongoDB instance for NoSQL data storage
3. **Data Preparation**: CSV files and JSON data prepared in `/data` directory
4. **Execution**: Jupyter notebook provides interactive ETL pipeline execution
5. **Validation**: Analytical queries verify data integrity and business logic
