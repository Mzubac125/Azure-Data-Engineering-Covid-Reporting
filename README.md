# Azure-Data-Engineering-Covid-Reporting

## Overview of Project
* This project entails acquiring multiple COVID-19 datasets from the ECDC website. These datasets are ingested using pipelines created in Azure Data Factory and stored in a bronze layer in a Azure Data Lake. They are then transformed using Databricks and stored back into the Data Lake in a silver layer. The processed data is subsequently loaded into a SQL Data Warehouse to enable the Analytics team to extract meaningful and actionable insights.

## Solution Arcitecture Overview

![Solution-Arcitecture](https://github.com/user-attachments/assets/30912068-c305-486e-83d0-8bb1a07fa9f0)


## Data Ingestion
Two datasets were ingested from the ECDC website, the cases and deaths data, and hospital admissions data.
Steps:
* Create a linked service to the HTTP source
* Create a source dataset
* Create a linked service to the data lake
* Create a sink dataset
* Create a pipelines that uses parameters and variables
* Use a json file to lookup all the values for the parameters then use a ForEach activity combined with a copy activity to copy both datasets to data lake
* Schedule a trigger

### Pipeline Design
<img width="1397" alt="PipelineDesignECDCData" src="https://github.com/user-attachments/assets/f8aa092a-102f-4b09-9c7b-67d1315546ae">

## Data Transformation
#### Hospital Admissions
* Select only the needed columns and make a new column for week
* Get the week start date from the date column
* Sum up the daily values and group by the week to create a new weekly table
* Pivot both tables to have the indicator value as a column
* Export both tables to the data lake
* Create another activity in ADF with triggers that will run the Databricks notebooks

## Create an Azure SQL Database and copy over the transformed Covid-19 data from the Data Lake
![sql db create table](https://github.com/user-attachments/assets/ff556cbe-7888-4fa1-88c7-94367d061470)
![sql database pl copy](https://github.com/user-attachments/assets/0a80819f-c7fa-48b3-887d-12ad1961d42a)

## Reporting with Power BI
* Create a connection from Azure SQL to Power BI
* Create Dashboard that analyzes the Covid-19 data we have gathered
