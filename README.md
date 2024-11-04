# Demo machine learning with snowflake snowpark

## Introduction

This repo contains some info to 
* Setup snowflake (for machine learning), 
* An example CSV cars data set
* A notebook demonstrating the use of [snowpark ML](https://docs.snowflake.com/en/developer-guide/snowflake-ml/overview). 

We'll train a machine learning model ( a regression model in this case) using a snowpark ML pipeline and register that pipeline in the snowpark model registery. The model can then be used for scoring new data. See the `carprice_prediction_snowflake_notebook.ipynb` notebook for more details.

## Setup your snowflake account

If you don't have a snowflake account yet, it is easy and fast (within 4 minutes) to create a [trial account](https://signup.snowflake.com/?trial=student). Register a trial without credit card details. You should have 120 days and 400 credits to do some experimention in snowflake


## Create database objects
In your snowflake environment it is good to separate this machine learning 'experiment' in a separate database. So lets create a new database called 'CARS_DATA'. 

1. Click on the '+ CREATE' button 
2. Select SQL worksheet 
3. In that new worksheet type in and run:

```sql
CREATE DATABASE CARS_DATA;
```

## Get the data and the notebook into snowflake

There are two ways to get the CSV data set and the notebook in this repo into your snowflake environment. 1. manualy upload the data and the notebook, or 2 via git integration.

###  1. Manually uploads 

#### Upload Data

Now that we have a database, we can populate it with tables, one way is to upload data. Download the [car_prices.csv](https://github.com/longhowlam/snowflake_cars_prediction/blob/main/car_prices.csv) data set from this repository. Then to upload the `car_prices.csv` dataset, you can use the Snowflake web interface. Below is an example of how to upload the data using the Snowflake web interface:

1. Navigate to the Data > Databases section,
2. Select the `CARS_DATA` database that we just created.
3. Select the `PUBLIC` schema,
3. Click on the CRAETE button and select Table from file.
4. Use the "Load Data" option to upload the `car_prices.csv` file.

Here are some screenshot of the upload process:



<img src="images\upload_data.png" alt="Upload Data" width="600" style="border: 2px solid black;"/>

<img src="images\upload_data_2.png" alt="Upload Data" width="600"/>

<img src="images\upload_data_3.png" alt="Upload Data" width="600"/>

When the data is uploaded you can view the car_price data in the snowflake interface

<img src="images\cars_data.png" alt="car price Data" width="600"/>


#### Upload Notebook

We can now upload the `carprice_prediction_snowflake_notebook.ipynb` in this repository to snowflake. From the snowflake homepage:
1. Click + Create
2. Select Notebookk > Import *.ipynb file 

<img src="images\createnotebook.png" alt="create notebook" width="250"/>

<img src="images\createnotebook_2.png" alt="create notebook" width="250"/>


### 2. Via Git integration in Snowflake

Snowflake allows you to clone git repositories from github or gitlab. In order to thatwe first need to create an API integration and the using that api integration, we can clone a repository (into a data base).

1. Click on the '+ CREATE' button 
2. Select SQL worksheet 
3. Select the database `CARS_DATA` and `PUBLIC` schema
3. In that new worksheet type in and run:

```sql
CREATE or REPLACE api integration git_api_integration
    api_provider = git_https_api
    api_allowed_prefixes = ('https://github.com/longhowlam/')
    enabled = true
    allowed_authentication_secrets = all
;
```

Run the above command to create an api integration, then we can clone this repo

```sql
CREATE OR REPLACE GIT REPOSITORY cars_prediction
    API_INTEGRATION = git_api_integration
    ORIGIN = 'https://github.com/longhowlam/snowflake_cars_prediction.git'
;
```

Now you should see the repo in your snowflake account, see a screenshot in the figure below.

<img src="images\gitrepo.png" alt="git repo" width="350"/>

Form there you can create the notebook in your snwoflake account by clicking on the three dots.

<img src="images\gitrepo2.png" alt="create notebook" width="400"/>

A dialog will appear where you can set the notebook runtime, and then you will see the notebook appear as a natibe snowflake notebook inside your snowflake environment. The notebook environment includes the `car_prices.csv` data set. This can be imported with pandas in the notebook and then the data can be put in a snowflake database with snowpark stateents. See notebook.


## Packages used by botebook

The notebooks inside the snowflake web interface make use of packages, some packages are already pre loaded, some need to be added. The notebook in this repo makes use of the `plotly` and the `snowflake-ml-python` packages we need to enter those in the package list of the notebook first.

<img src="images\packages.png" alt="Upload Data" width="250"/>

Now you can run the cells in the notebook and get an idea of snowpark ML.



