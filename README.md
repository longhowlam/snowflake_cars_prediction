# Demo snowflake notebook on snowpark ML

## Intro

This repo contains a script and a notebook demonstrating the use of [snowpark ML](https://docs.snowflake.com/en/developer-guide/snowflake-ml/overview).

## Setup account

If you don't have a snowflake account yet, it is easy create a [trial account](https://signup.snowflake.com/?trial=student). You should have 120 days and 400 credits to do some experimention.


## Create database objects

Lets create a new database called 'CARS_DATA'. 
1. Click on the '+ CREATE' button 
2. Select SQL worksheet 
3. In that new worksheet type in and run:

```sql
CREATE DATABASE CARS_DATA;
```



## Upload Data

Now that we have a database, we can populate it with tables, one way is to upload data. To upload the `car_prices.csv` dataset, you can use the Snowflake web interface or the SnowSQL command line tool. Below is an example of how to upload the data using the Snowflake web interface:

1. Navigate to the "Databases" tab.
2. Select the `CARS_DATA` database.
3. Click on the "Tables" section and create a new table to hold the car prices data.
4. Use the "Load Data" option to upload the `car_prices.csv` file.

Here are some screenshot of the upload process:

![Upload Data](upload_data.png)

![Upload Data](upload_data_2.png)

![Upload Data](upload_data_3.png)



## Notebook


