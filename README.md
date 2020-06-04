# Project: Data Modeling with Cassandra

## Introduction

<p>A startup called Sparkify wants to analyze the data they've been collecting on songs and user activity on their new music streaming app. The analysis team is particularly interested in understanding what songs users are listening to. Currently, there is no easy way to query the data to generate the results, since the data reside in a directory of CSV files on user activity on the app.</p>

<p>They'd like a data engineer to create an Apache Cassandra database which can create queries on song play data to answer the questions. </p>

## Project Datasets

For this project, you'll be working with one dataset: **event_data**. The directory of CSV files partitioned by date. Here are examples of filepaths to two files in the dataset:

>**event_data/2018-11-08-events.csv**<br>
>**event_data/2018-11-09-events.csv**

Below is an example of what an original single event data file, **2018-11-08-events.csv**, looks like.
```
{
    "artist": "Slipknot", 
    "auth": "Logged In", 
    "firstName": "Aiden", 
    "gender": "M", 
    "itemInSession": 0, 
    "lastName": "Ramirez", 
    "length": 192.57424, 
    "lvevel": "paid", 
    "location": "New York-Newark-Jersey City,NY-NJ-PA"
    "method": "PUT"    
    "page": "NextSong"
    "regisgration":1.54028E+12
    "sessionId":19
    "song":"Opinum Of The People"
    "status":200
    "ts":1.5416E+12
    "userId":20    
}
```

##  ETL Pipeline for Pre-Processing the Files

Processing the original event data files to create the **event_datafile_new.csv** that will be used for creating Apache Casssandra tables

The **event_datafile_new.csv** contains the following columns:

>**artist<br>
firstName<br>
gender<br>
itemInSession<br>
lastName<br>
length<br>
level<br>
location<br>
sessionId<br>
song<br>
>userId**<br>


## Data Modeling 

With Apache Cassandra, the database tables are modelled on the requested queries.

**1. Give me the artist, song title and song's length in the music app history that was heard during sessionId = 338, and itemInSession = 4**<br>

```
Create table sessions
    (
        sessionId int,
        itemInSession int,
        artist_name text,
        song text,
        song_length float,
        PRIMARY KEY (sessionId, itemInSession)  
    ) WITH CLUSTERING ORDER BY (itemInSession DESC)
```

**2. Give me only the following: name of artist, song (sorted by itemInSession) and user (first and last name) for userid = 10, sessionid = 182**<br>

```
Create table song_play_list
    (
        userid int,
        sessionid int,
        iteminsession int,
        firstname text,
        lastname text,      
        artist_name text,
        song text,     
        PRIMARY KEY((userid, sessionid), iteminsession)
     ) WITH CLUSTERING ORDER BY (iteminsession DESC)

```

    
**3. Give me every user name (first and last) in my music app history who listened to the song 'All Hands Against His Own'**<br>

```
Create table users_playlist 
    (
        song text,
        user_id,
        firstname text,
        lastname text,  
        PRIMARY KEY (song, user_id)  
    ) WITH CLUSTERING ORDER BY (user_id DESC)
```

## Build ETL Pipeline

**1. Include Apache Cassandra *CREATE* statements to create relevant tables for the above data model** 


**2. Include Apache Cassandra *INSERT* statements to load processed records into relevant tables from dataset *event_datafile_new.csv***


**3. Add in the *SELECT* statement to verify the data was entered into the table**


## Project Files

In addition to the data files, the project workspace includes 3 files:<br>
**2. Project_1B_ Data_Modelling_With_Cassandra.ipynb**  Create a denormalized dataset, load the data into tables and run test queries <br>


**3. README.md**                                        Provide project info <br>


## Author

**Xingya Zhou**
    
    
 
