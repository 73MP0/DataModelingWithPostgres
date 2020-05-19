# Data Modeling
A startup called Sparkify wants to analyze the data they've been collecting on songs and user activity on their new music streaming app. The analytics team is particularly interested in understanding what songs users are listening to. Currently, they don't have an easy way to query their data, which resides in a directory of JSON logs on user activity on the app, as well as a directory with JSON metadata on the songs in their app.

# Database Schema
Fact Table
- songplays - records in log data associated with song plays i.e. records with page NextSong
    - songplay_id, start_time, user_id, level, song_id, artist_id, session_id, location, user_agent

Dimension Tables
- users - users in the app
    - user_id, first_name, last_name, gender, level
- songs - songs in music database
    - song_id, title, artist_id, year, duration
- artists - artists in music database
    - artist_id, name, location, latitude, longitude
- time - timestamps of records in songplays broken down into specific units
    - start_time, hour, day, week, month, year, weekday

# sql_queries.py
DROP TABLES
- set of drop commands saved in variables to drop the table if it already exists
CREATE TABLES
- table creation queries saved in variables for each table.
INSERT RECORDS
- insert commands used to make writes to the tables.
FIND SONGS
- query used to find the song to insert to the fact table
QUERY LISTS
- variables used to put the drop and create commands into a set.

# etl.ipynb
Python notebook used to build the blueprint for the ETL program that will automate the data pipeline. The notebook documents the steps required to insert data into the databases.

# etl.py
ETL pipeline that will insert all the required data into the database. The program is broken down into 3 main functions that are used in Main.
- process_song_file
    - takes in cursor and filepath arguments
    - open song file
    - insert song record
    - insert artist record
- process_log_file
    - takes in cursor and filepath arguments.
    - open log file.
    - filter by NextSong action
    - format time data
    - insert user/songplay records
- process_data
    - takes in cursor, connection, filepath, and function arguments
    - get all files matching extension from directory
    - get total number of files found
    - iterate over files and process
