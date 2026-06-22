Overview:
This project is an automated Data Engineering pipeline designed to extract, transform, and load (ETL) daily e-commerce order data from cloud storage into a structured relational data warehouse.
Key Features & Architecture:
Extraction: Connects to an AWS S3 bucket using boto3 to fetch raw, nested JSON files partitioned by the current date.
Transformation: Utilizes pandas to parse and flatten the nested JSON data, separating it into distinct entities: Customers, Products, and Orders. The step includes data cleaning, deduplication, and sorting.
Loading & Warehousing: Uses SQLAlchemy to load the transformed DataFrames into a MySQL database. It employs a Star Schema design, generating Surrogate Keys for dimensional tables (dim_customers, dim_products) and populating a central fact table (fact_orders).
Slowly Changing Dimensions (SCD): Implements SCD Type 1 for customer records (overwriting old data with new addresses/emails) and SCD Type 2 for product records (maintaining historical pricing/category data using effective start and end dates).
