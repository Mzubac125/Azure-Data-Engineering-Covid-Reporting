# Azure-Data-Engineering-Covid-Reporting

## Overview of Project
* This project entails acquiring multiple COVID-19 datasets from the ECDC website. These datasets are ingested using pipelines created in Azure Data Factory and stored in a bronze layer in a Azure Data Lake. They are then transformed using Databricks and stored back into the Data Lake in a silver layer. The processed data is subsequently loaded into a SQL Data Warehouse to enable the Analytics team to extract meaningful and actionable insights.

* 
