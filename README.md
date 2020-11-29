# Data Modeling with PostgreSQL



## Content
- [Description](#description)
- [Data](#data)
- [PostgreSQL Database](#postgresql-database)
- [Workflow](#workflow)
- [Repository Organization](#repository-organization)
- [Links](#links)

## Description  

In this project I used Python to build an ETL pipeline and PostgreSQL to show data modeling. The subject of the project is the fictional music streaming provider "Sparkify", which is in need of a database to analyze their data generated from the app.  
The final database 'sparkifydb' is build in a star schema with fact and dimension tables. The main goal is it to create a database with tables designed to optimize queries on songplay analysis.

## Data  

The data used for this project consists out of two directories. The log_data are .json files with data on user activity on the app and the song_data which are also .json files with metadata on songs in the app. 
The song data files are only a small subset of the original [million songs dataset](http://millionsongdataset.com). The log data was created with the help of this [eventsimulator](https://github.com/Interana/eventsim) and based on the song data. All data was provided by Udacity as part of the data engineer nanodegree. 

## PostgreSQL Database  

The database is named "sparkifydb" and consists out of the following tables:  

- fact table: songplays (records in the log data associated with song plays)  
    columns: *songplay_id, start_time, user_id, level, song_id, artist_id, session_id, location, user_agent*

- dimension table: users (data on app users)  
    columns: *user_id, first_name, last_name, gender, level*

- dimension table: songs (data on all songs in library/app)  
    columns: *song_id, title, artist_id, year, duration*

- dimension table: artists (data on all artists in library/app)  
    columns: *artist_id, name, location, latitude, longitude*

- dimension table: time (timestamps of songplays in log data brocken down in different units)  
    columns: *start_time, hour, day, week, month, year, weekday*


## Workflow
  
1) I started out with writing the SQL queries to create the tables in sql_queries.py   
  example: 
  `songplay_table_create = ("""CREATE TABLE IF NOT EXISTS songplays(songplay_id SERIAL PRIMARY KEY,\
                                start_time bigint NOT NULL, user_id int NOT NULL, level varchar , \
                                song_id varchar, artist_id varchar, session_id int, \
                                location varchar, user_agent varchar)`
  
2) Afterwards I added the drop table queries. They are necessary in the create_table.py in order to drop the existing tables before they are created again.   
  example: 
  `songplay_table_drop = "DROP TABLE IF EXISTS songplays"`
  
3) In the etl.ipynb I developed the etl processes for the different tables and used that code to finalize the etl.py to build the pipeline. In between I used the test.ipynb to varify the different steps and check if the code worked as expected. 
  
4) In the end I confirmed that the process is successfull by running the files in this order:
- create_tables.py
- etl.py
- test.ipynb (for confirmation)


## Repository Organization

1) The data directory contains seperate directories for the song data and log data
  
2) The notebooks directory contains two Jupyter Notebooks. The etl.ipynb was used to build and test step by step the etl code which was than used in the etl.py to build the pipeline. The test.ipynb was used to test the code in the etl.ipynb, sql_queries.py and etl.py files. 

3) The python files consist out of the create_tables.py which creates the sparkify database and necessary tables, the etl.py which extracts the data from the data files and inserts them into the database and the sql_queries.py with the postgres queries used in create_tables.py and etl.py


## Links

[Repository](https://github.com/Ulli-H/Data_Modeling_Postgres)  
