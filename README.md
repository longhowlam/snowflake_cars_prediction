# Demo machine learning with snowflake snopwarkwpark

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

There are two ways to get the CSV data set and the notebook in this repo into your snowflake environment. 

###  1. Manually uploads 

#### Upload Data

Now that we have a database, we can populate it with tables, one way is to upload data. Download the [car_prices.csv](https://github.com/longhowlam/snowflake_cars_prediction/blob/main/car_prices.csv) data set from this repository. Then to upload the `car_prices.csv` dataset, you can use the Snowflake web interface. Below is an example of how to upload the data using the Snowflake web interface:

1. Navigate to the Data > Databases section,
2. Select the `CARS_DATA` database that we just created.
3. Select the `PUBLIC` schema,
3. Click on the CRAETE button and select Table from file.
4. Use the "Load Data" option to upload the `car_prices.csv` file.

Here are some screenshot of the upload process:

<img src="images\upload_data.png" alt="Upload Data" width="600"/>

<img src="images\upload_data_2.png" alt="Upload Data" width="600"/>

<img src="images\upload_data_3.png" alt="Upload Data" width="600"/>

When the data is uploaded you can view the car_price data in the snowflake interface

<img src="images\cars_data.png" alt="car price Data" width="600"/>


#### Upload Notebook

We can now upload the `carprice_prediction_snowflake_notebook.ipynb` in this repository to snowflake. From the snowflake homepage:
1. Click + Create
2. Select Notebookk > Import *.ipynb file 

<img src="images\createnotebook.png" alt="Upload Data" width="250"/>

<img src="images\createnotebook_2.png" alt="Upload Data" width="250"/>


### 2. Via Git integration in Snowflake

to be filled....

## Packages used by botebook

The notebooks inside the snowflake web interface make use of packages, some packages are already pre loaded, some need to be added. The notebook in this repo makes use of the `plotly` and the `snowflake-ml-python` packages we need to enter those in the package list of the notebook first.

<img src="images\packages.png" alt="Upload Data" width="250"/>

Now you can run the cells in the notebook and get an idea of snowpark ML.



