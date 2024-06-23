# Azure Data Engineering Project - Adventure Works Sample Data
This project aims to create an end-to-end data pipeline from ingestion data to visualization by leveraging various Azure services with the Adventure Works sample data.

## Data Source
[Adventure Works Sample Dataset](https://learn.microsoft.com/en-us/sql/samples/adventureworks-install-configure?view=sql-server-ver16&tabs=ssms)

## Data Pipeline Architecture
![image](https://github.com/AdamChan-ML/adventureworks-datapipeline/assets/78518992/7f8d3fe5-ed14-48d8-939f-0dffa8dde0e2)

## Data Model / Schema
![image](https://github.com/AdamChan-ML/adventureworks-datapipeline/assets/78518992/79569a89-359b-4cca-9e84-7505bce1613f)

## Storage File Structure
- layer/schemaName/tableName/table.parquet (E.g. bronze/SalesLT/Customer/Customer.parquet)

## Setup: Restore Adventure Works database in Azure SQL database
* MS SQL would not work for Mac user as it cannot be connected to azure data factory due to the limitation of azure data studio (self-hosted integration runtime N/A)
![image](https://github.com/AdamChan-ML/adventureworks-datapipeline/assets/78518992/9856efd2-4f36-4c1a-b0d1-f2f9d0de4150)

## Data Ingestion: Ingest Data from Azure SQL (act as on-prem database) to Bronze Layer Azure Data Lake Storage Gen 2
![image](https://github.com/AdamChan-ML/adventureworks-datapipeline/assets/78518992/dae47e87-590c-4bcc-86eb-d86ba1a228ce)

## Data Transformation: Perform data transformation from bronze to silver layer and silver to gold layer
- Bronze --> Silver: Transform date column into date format as the date columns in every table is in datetime format in default
- Silver --> Gold: Convert every column naming format from ColumnName to Column_Name for better naming conventions
![image](https://github.com/AdamChan-ML/adventureworks-datapipeline/assets/78518992/4d203269-0c3a-44d7-a25e-938add19b63d)

## Data Loading: Load the gold table into Azure Synapse to create views for each table
- Stored procedure is created to create a view for every tables in the gold layer and it can be run whenever there's a data schema changes.
![image](https://github.com/AdamChan-ML/adventureworks-datapipeline/assets/78518992/a07edb93-707e-40db-890f-27910de16839)

## Data Visualization
- A sales dashboard for adventure works is created by direct quering the data from Azure Synapse Analytics
![image](https://github.com/AdamChan-ML/adventureworks-datapipeline/assets/78518992/bb9ff5b1-9893-477b-9e49-6ce8da64c264)

## Data Pipeline Testing
- Add a schedule trigger to run the pipeline in a daily basis
- Insert new rows into the stimulated on-premise database

![image](https://github.com/AdamChan-ML/adventureworks-datapipeline/assets/78518992/76d52982-edf3-47d4-87b5-6e248d6b2412)
![image](https://github.com/AdamChan-ML/adventureworks-datapipeline/assets/78518992/506e8b99-d814-4bb4-b167-8f1e69ac1549)

## Resource group used in the project
![image](https://github.com/AdamChan-ML/adventureworks-datapipeline/assets/78518992/3f11f855-4b58-4429-bda8-9a92fd7faa97)

