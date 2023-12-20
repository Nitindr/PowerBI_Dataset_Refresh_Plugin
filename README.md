# Airflow Power BI Dataset Refresh Operator

This repository contains a custom Apache Airflow operator (`PowerBIDatasetRefreshOperator`) designed for refreshing Power BI datasets using the Power BI REST API.

## Overview

The `PowerBIDatasetRefreshOperator` is a custom Apache Airflow operator that allows you to automate the refresh of a Power BI dataset from within your Airflow DAGs. It leverages the Microsoft Authentication Library (MSAL) to obtain an access token and interacts with the Power BI REST API to check and trigger dataset refreshes.

## Prerequisites

Before using the operator, make sure you have the following prerequisites:

- Power BI workspace and dataset information.
- Azure AD application Registered with the required permissions for the Power BI service.
- Python environment with necessary dependencies installed.

## Usage
1. Place this plugin in your plugins folder of your Apache Airflow
```
   ex: /usr/local/airflow/plugins/powerbi_plugin
```
If you are using AWS MWAA we need the package the operator in a zip file and need to place the plugins.zip file in the plugins folder
```
   ex: /usr/local/airflow/plugins/plugins.zip
```
The folder structure looks similar to below represantation
```
├── dags
│   └── powerbi_dataset_refresh_dag.py  
├── plugins
│   └── __init__.py
|   └── powerbi_plugin
|       └──__init__.py
|       └──operators
           └──__init__.py
           └──powerbi_dataset_refresh_operator.py
```
           

2. Import the PowerBIDatasetRefreshOperator in your Airflow DAG file:
```
   from airflow.models import DAG
   from airflow.operators.powerbi_refresh_operator import PowerBIDatasetRefreshOperator
```

3. Create a task for the Custom Operator within your DAG:
```
refresh_powerbi_dataset = PowerBIDatasetRefreshOperator(
   task_id='refresh_powerbi_dataset',
   client_id='your_client_id',
   client_secret='your_client_secret',
   tenant_name='your_tenant_name',
   workspace_id='your_workspace_id',
   dataset_id='your_dataset_id',
   dag=dag,
)
```

## Configuration
```
client_id: The client ID of your Azure AD application.
client_secret: The client secret of your Azure AD application.
tenant_name: The name of your Azure AD tenant.
workspace_id: The Power BI workspace ID.
dataset_id: The Power BI dataset ID.
```
