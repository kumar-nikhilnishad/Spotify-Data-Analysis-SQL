# Spotify-Data-Analysis-SQL
This project involves performing data exploration and analysis on a real-world Spotify music dataset using PostgreSQL. The goal is to extract meaningful insights from the dataset by leveraging SQL techniques including Window Functions, CTEs, Aggregations, and Filtering.
________________________________________
## Dataset Overview
The dataset contains various attributes of music tracks including:

•	artist, track, album, album_type

•	Audio features: danceability, energy, loudness, speechiness, acousticness, instrumentalness, liveness, valence, tempo

•	Metadata: duration_min, title, channel, views, likes, comments

•	Flags: licensed, official_video

•	stream, most_playedon, energyliveness (calculated)
________________________________________
## Key SQL Concepts Applied
•	Exploratory Data Analysis (EDA)

•	Aggregation & Grouping

•	Filtering & Conditions

•	Common Table Expressions (CTEs)

•	Window Functions (e.g., SUM() OVER, DENSE_RANK() OVER)

•	Subqueries
________________________________________
## Analysis Highlights
1.	Tracks with over 1 Billion Streams
2.	Top Tracks by Energy and Danceability
3.	Total Comments for Licensed Tracks
4.	Tracks Streamed More on Spotify vs. YouTube
5.	Energy-to-Liveness Ratio > 1.2
6.	Cumulative Likes Ordered by Views
7.	Top 3 Most Viewed Tracks per Artist
8.	Liveness Scores Above Average
9.	Energy Range (Max - Min) Per Album
________________________________________
## Sample Advanced Queries
### 1. Top 3 most-viewed tracks for each artist using window functions.
WITH CTE

 AS

(

SELECT

      artist,
	  track,
	  SUM(views) AS total_view,
	  DENSE_RANK() OVER(PARTITION BY artist ORDER BY SUM(views) DESC) AS rank

FROM spotify

GROUP BY 1,2

)

 SELECT * FROM CTE

 WHERE rank <= 3;

### 2. Cumulative Likes by Views
SELECT

    track,
    views,
    likes,
    SUM(likes) OVER (ORDER BY views DESC) AS cumulative_likes
FROM spotify

GROUP BY 1, 2, 3;

### 3. Energy-to-Liveness Ratio
WITH CTE 

AS 

(

    SELECT
                track,
                energy,
                liveness,
                (energy / liveness) AS energy_to_liveness_ratio
    FROM spotify
)

SELECT

    track,
    energy_to_liveness_ratio
FROM CTE

WHERE energy_to_liveness_ratio > 1.2

    AND liveness <> 0;
________________________________________
## Tech Stack
•	Database: PostgreSQL

•	Language: SQL

•	Tools: pgAdmin / DBeaver / psql
________________________________________
## How to Use
1.	Import the spotify dataset into your PostgreSQL instance.
2.	Run the SQL queries from the provided .docx or .sql file.
3.	Explore and extend the analysis with your own queries.


________________________________________
## Contact
If you have feedback, questions, or collaboration ideas, feel free to connect with me on https://www.linkedin.com/in/nikhil-kumar-3982a9348/.



💬 Always happy to connect with fellow data enthusiasts and professionals!
