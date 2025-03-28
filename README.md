# spotify_Data-Anaytiys
Analysis spotify Exploratory Data Analysis (EDA) ,Find impact full inshights

Downlaod Data from Github:https://github.com/najirh/najirh-Spotify-Data-Analysis-using-SQL/tree/main

![spotify](https://github.com/saurav190101/spotify_Data-Anaytiys/blob/main/spotify.png)

**create Table**
```
CREATE TABLE spotify (
    artist VARCHAR(255),
    track VARCHAR(255),
    album VARCHAR(255),
    album_type VARCHAR(50),
    danceability FLOAT,
    energy FLOAT,
    loudness FLOAT,
    speechiness FLOAT,
    acousticness FLOAT,
    instrumentalness FLOAT,
    liveness FLOAT,
    valence FLOAT,
    tempo FLOAT,
    duration_min FLOAT,
    title VARCHAR(255),
    channel VARCHAR(255),
    views FLOAT,
    likes BIGINT,
    comments BIGINT,
    licensed BOOLEAN,
    official_video BOOLEAN,
    stream BIGINT,
    energy_liveness FLOAT,
    most_played_on VARCHAR(50)
);
```

File :Spotify.csv


:hammer_and_wrench:**Tech Stack Used:**

***SQL:** PostgreSQL, Joins, CTEs, Window Functions, Aggregations 

## 📊 Key Insights & Business Impact

1.Count the total number of tracks by each artist.

--Figure out artists which have highest  total track 

2.Retrieve the track names that have been streamed on Spotify more than YouTube.

--Analyze between spotify and youtube which one people like most to  stramed 

3.Find the top 5 tracks with the highest energy values.

--Analyze Tracks which have energetic tracks feel fast, loud, and noisy. 

----

## 🔥 SQL Analysis Highlights

**Find the top 3 most-viewed tracks for each artist using window functions.**
```
select * from (
select artist,track,sum(views) total_views
,dense_rank()over(partition by artist order by sum(views)desc ) as drn 
from spotify 
group by 1,2
) where drn between 1 and 3;
```

**calculate the difference between the highest and lowest energy values for tracks in each album.**
```
with diffrence as(
select album, max(energy) highest_energy,min(energy)as 
lowest_energy from spotify
group by 1)
select album, highest_energy-lowest_energy as diffrences
from diffrence
order by 2 desc;
```
---
