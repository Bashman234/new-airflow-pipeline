
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

- GCP account

**Project Setup**
- Download the dataset https://www.kaggle.com/datasets/tunguz/online-retail
- Store the csv file in `include/dataset/online_retail.csv`
- In requirements.txt, add `apache-airflow-providers-google==10.3.0` restart Airflow.
- Create a GCS bucket with a unique name `<your_name>_online_retail`
- Create a service account with a name `airflow-online-retail`
- Grant admin access to GCS + BigQuery
- Click on the service account → Keys → Add Key → Copy the JSON content
-  Create a new file `service_account.json` in `include/gcp/`
- Airflow → Admin → Connections
    - id: gcp
    - type: Google Cloud
    - Keypath Path: `/usr/local/airflow/include/gcp/service_account.json`
- Test the connection → Save (**from 2.7 must be turned on**)
- Create the DAG
- Create an empty Dataset (schema equivalent)`from airflow.providers.google.cloud.operators.bigquery import BigQueryCreateEmptyDatasetOperator`
- Create the task to load the file into a BigQuery raw_invoices table
- Data loaded into the warehouse

**Transformation**
- install Cosmo - DBT in requirements.txt
- in Dockerfile install dbt into a virtual environment
- Restart astro cli with command astro dev restart
- Create `include/dbt` folder and add `packages.yml`, `dbt_project.yml` and `profiles.yml`
- In Bigquery copy and excute the following request to create countries table:
https://docs.google.com/document/d/e/2PACX-1vSJGbKBIJsFX7v3uWtB8IryVgFlr99NzXai6uvHQhOQ9JHxCOrZ_71_4peVRGmRNUS2UH043D63nAKS/pub
- create `models/sources`
- create `models/transfrom` with the following transformation files
    - dim_customer.sql
    - dim_datetime.sql
    - dim_product.sql
    - fct_invoices.sql
- Run the models in a virtual new python env you create inside the astro cli
- use commands
`astro dev bash
python3 venv -m newenv
source newenv/bin/activate
cd include/dbt 
dbt deps
dbt run --profiles-dir /usr/local/airflow/include/dbt/`
-Check on Bigquery that the tables exist with data
**Reports**
  - in `include/dbt/models/report` create the following files
      - report_customer_invoices.sql
      - report_product_invoices.sql
      - report_year_invoices.sql
test final dbt run
`astro dev bash
cd include/dbt
python3 venv -m newenv
source newenv/bin/activate
cd include/dbt 
dbt run --select path:models/report --profiles-dir /usr/local/airflow/include/dbt/`
- use docker compose create a metabase dashboard
- data pipeline is complete


