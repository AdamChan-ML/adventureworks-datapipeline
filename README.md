# Azure Data Engineering Project - Adventure Works Sample Data
This project aims to create an end-to-end data pipeline from ingestion data to visualization by leveraging various Azure services with the Adventure Works sample data. The pipeline will be triggered in a daily basis, and the latest updated data will be reflected in the dashboard automatically. 

## Data Source
[Adventure Works Sample Dataset](https://learn.microsoft.com/en-us/sql/samples/adventureworks-install-configure?view=sql-server-ver16&tabs=ssms)
- "The AdventureWorks databases are sample databases that were originally published by Microsoft to show how to design a SQL Server database using SQL Server 2008."

## Data Pipeline Architecture
![image](https://github.com/AdamChan-ML/adventureworks-datapipeline/assets/78518992/7f8d3fe5-ed14-48d8-939f-0dffa8dde0e2)
- On-premise Database Simulation: Azure SQL, Microsft SQL Server, Docker, Azure Data Studio
- Data Ingestion: Azure Data Factory
- Data Transformation: Azure Databricks
- Data Loading: Azure Synapse Analytics
- Data Visualization: Microsoft PowerBI
- Data Storage: Azure SQL, Azure Data Lake Storage Gen 2
- Data Security & Governance: Azure Key Vault

## Data Model / Schema
![image](https://github.com/AdamChan-ML/adventureworks-datapipeline/assets/78518992/79569a89-359b-4cca-9e84-7505bce1613f)

## Storage File Structure
- layer/schemaName/tableName/table.parquet (E.g. bronze/SalesLT/Customer/Customer.parquet)

## Setup On-premise database
- Restore Adventure Works database in Azure SQL database
- Connect Azure SQL to Azure Data Studio
- * MS SQL would not work for Mac user as it cannot be connected to azure data factory due to the limitation of azure data studio (self-hosted integration runtime N/A)
![image](https://github.com/AdamChan-ML/adventureworks-datapipeline/assets/78518992/9856efd2-4f36-4c1a-b0d1-f2f9d0de4150)

## Data Ingestion
- Ingest data from Azure SQL (act as on-prem database) to bronze layer in Azure Data Lake Storage Gen 2
![image](https://github.com/AdamChan-ML/adventureworks-datapipeline/assets/78518992/dae47e87-590c-4bcc-86eb-d86ba1a228ce)

## Data Transformation
- Bronze --> Silver: Transform date column into date format as the date columns in every table is in datetime format in default
- Silver --> Gold: Convert every column naming format from ColumnName to Column_Name for better naming conventions
![image](https://github.com/AdamChan-ML/adventureworks-datapipeline/assets/78518992/4d203269-0c3a-44d7-a25e-938add19b63d)

## Data Loading: Load the gold table into Azure Synapse to create views for each table
- Stored procedure is created to create a view for every tables in the gold layer and it can be run whenever there's a data schema changes.
![image](https://github.com/AdamChan-ML/adventureworks-datapipeline/assets/78518992/a07edb93-707e-40db-890f-27910de16839)

## Data Visualization
- A sales dashboard for adventure works is created by direct quering the data from Azure Synapse Analytics
![image](https://github.com/AdamChan-ML/adventureworks-datapipeline/assets/78518992/bb9ff5b1-9893-477b-9e49-6ce8da64c264)

## Result: Data Pipeline Testing
- The pipeline is scheduled to be triggered in a daily basis
- Insert new rows into the simulated on-premise database
- The dashboard will automatically reflected and updated based on the latest data
![image](https://github.com/AdamChan-ML/adventureworks-datapipeline/assets/78518992/76d52982-edf3-47d4-87b5-6e248d6b2412)
![image](https://github.com/AdamChan-ML/adventureworks-datapipeline/assets/78518992/506e8b99-d814-4bb4-b167-8f1e69ac1549)

## Resource group used in the project
![image](https://github.com/AdamChan-ML/adventureworks-datapipeline/assets/78518992/3f11f855-4b58-4429-bda8-9a92fd7faa97)

## For more detailed documentation:
- [Documentation]()

