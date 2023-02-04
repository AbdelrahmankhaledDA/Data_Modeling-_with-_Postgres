#Sparkify

This project is to apply data modeling with Postgres and build ETL pipeline with Python.
Project Description

We will use two datasets: Songs dataset and Logs dataset

#Songs dataset

Each file on the path data/song_data contains the following JSON object:

{
    "num_songs": 1,
    "artist_id": "AR7G5I41187FB4CE6C",
    "artist_latitude": null,
    "artist_longitude": null,
    "artist_location": "London, England",
    "artist_name": "Adam Ant",
    "song_id": "SONHOTT12A8C13493C",
    "title": "Something Girls",
    "duration": 233.40363,
    "year": 1982
}

#Logs dataset

Each file on the path data/log_data contains a list of the following object:

{
    "artist": null,
    "auth": "Logged In",
    "firstName": "Walter",
    "gender": "M",
    "itemInSession": 0,
    "lastName": "Frye",
    "length": null,
    "level": "free",
    "location": "San Francisco-Oakland-Hayward, CA",
    "method": "GET",
    "page": "Home",
    "registration": 1540919166796.0,
    "sessionId": 38,
    "song": null,
    "status": 200,
    "ts": 1541105830796,
    "userAgent": "\"Mozilla/5.0 (Macintosh; Intel Mac OS X 10_9_4) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/36.0.1985.143 Safari/537.36\"",
    "userId": "39"
}

#Schema

#Songplays (fact table)

(songplay_id INT PRIMARY KEY,
start_time BIGINT NOTNULL,
user_id int,
level varchar,
song_id varchar NOT NULL,
artist_id varchar NOT NULL,
session_id int,
location varchar,
user_agent varchar
);

#Artists (dimension table)

(artist_id varchar PRIMARY KEY,
name varchar NOT NULL,
location varchar,
latitude numeric,
longitude numeric
);



#Songs (dimension table)

(song_id varchar PRIMARY KEY,
title varchar,
artist_id varchar,
year int,
duration numeric
);

#Time (dimension table)

(
        start_time BIGINT PRIMARY KEY,
        hour int,
        day int,
        week int,
        month int,
        year int,
        weekday varchar
);

#Users (dimension table)

(  user_id varchar PRIMARY KEY,
first_name varchar,
last_name varchar,
gender varchar,
level varchar
);

#Process

To create the database and tables we have a python script: create_tables.py which will import all the queries stored in sql_queries and will execute them. First it will drop all existing tables and the database if yhey exist, then it will create the database and each table.

Each table has a unique index (Primar Key) which it will get from the data obtained on the ETL process, on the case of the table time we are using the data type serial primary key to allow postgressql to increment the time_id value for every record inserted afterwards.

The script etl.py provides all the functions to perform the ETL process.

The scripts will be run by using terminals
