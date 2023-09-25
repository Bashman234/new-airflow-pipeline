
# Data Engineer Project: An end-to-end Airflow data pipeline with BigQuery, dbt

The goal of this project was to develope a workflow to extracts, transforms, and loads data. This workflow will allow users to analyse transcational data from an online retail store through a dashboard. Using Apache airflow for the workflow orchestration, along with docker to manage the various standardized unit containers.


## Dataset

This pipeline draws on transnational data set which contains all the transactions occurring between 01/12/2010 and 09/12/2011 for a UK-based and registered non-store online retail. The company mainly sells unique all-occasion gifts. Many customers of the company are wholesalers. the pipeline ingests the raw data into a google cloud bucket.

![App Screenshot](https://github.com/Bashman234/new-airflow-pipeline/blob/main/screenshots/Screenshot%202023-09-24%20at%2009.34.38.png)




## Tech Stack

**Cloud:** Google Cloud

**Data Lake:** Google Cloud Storage

**Data Warehouse:** Google BigQuery

**ETL:** DBT

**Data Visualization:** Metabase




## Project Architecture

![App Screenshot](https://github.com/Bashman234/new-airflow-pipeline/blob/main/screenshots/Screenshot%202023-09-25%20at%2012.18.36.png)


## Data Modeling


![App Screenshot](https://github.com/Bashman234/new-airflow-pipeline/blob/main/screenshots/Screenshot%202023-09-23%20at%2019.49.06.png)
## dashboard


![App Screenshot](https://github.com/Bashman234/new-airflow-pipeline/blob/main/screenshots/Screenshot%202023-09-23%20at%2019.38.47.png)

Dashboard can be viewed at this Link:
http://localhost:3000/public/dashboard/ebaaa392-1885-4590-93e4-52447b924673

## Reproducibility 

**Pre-requisites:** 
Make sure you have the following pre-installed components:

- Docker

- Astr CLI

- GCP account*
