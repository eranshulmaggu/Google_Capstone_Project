|                              Title                              |     Author   |    Date   |
|:----------------------------------------------------------------| :------------| :---------|
|Case Study: How does a bike-share company navigate speedy success| Anshul Maggu | 2025-04-29|

# Case Study: How does a bike-share company navigate speedy success

**Author**: Anshul Maggu    **Date**: 2025-04-29
## Background
Cyclistic: A bike-share program that features more than 5,800 bicycles and 600 docking stations. Cyclistic sets itself apart by also offering reclining bikes, hand tricycles, and cargo bikes, making bike-share more inclusive to people with disabilities and riders who can't use a standard two-wheeled bike. The majority of riders opt for traditional bikes; about 8% of riders use the assistive options. Cyclistic users are more likely to ride for leisure, but about 30% use them to commute to work each day.

Customers who purchase single-ride or full-day passes are referred to as casual riders. Customers who purchase annual memberships are Cyclistic members. Cyclistic's finance analysts have concluded that annual members are much more profitable than casual riders.

Moreno (Director of Marketing) has set a clear goal: Design marketing strategies aimed at converting casual riders into annual members. In order to do that, however, the marketing analyst team needs to better understand how annual members and casual riders differ, why casual riders would buy a membership, and how digital media could affect their marketing tactics. Moreno and her team are interested in analyzing the Cyclistic historical bike trip data to identify trends.

## Step 1: Getting Information of The Task
## Business Task
To identify how do annual members and casual rider s use Cyclistic differently.

## Stakeholders
Primary: Lily Monero, Director of Marketing

Secondary: Cyclistic executive team (approves recommended marketing program)

## Step 2: Collection and Preparation of Data

## Data & Source Integrity
* Data is stored in remote server [url](https://divvy-tripdata.s3.amazonaws.com/index.html) and provided by Motivate International Inc. and separated in chunks of querterly .csv files.
* Data has been protected under data-privacy license mentioned here: [license](https://divvybikes.com/data-license-agreement). This license states that this data has been provided "As is" as per bikeshares sole discretion. So reliability of the data can be vetted eventhough this has been provided by third party.
* This data cannot be connected to the individual riders and their credit card numbers as unique rider ID has been used to record ride data.

## Observations
1.  There are 13 columns in the data files. These are: ride_id, rideable_type, started_at, ended_at, start_station_name, end_station_name, start_station_id, end_station_id, start_station, start_lat, start_lng, end_lat, end_lng, member_casual

2.  started_at and ended_at columns contains date-time data and formatted as YYYY-MM-DD HH:MM:SS format.

3.  start_station_id and end_station_id has discrepancy. Some of the IDs contain alphabets at the beginning (12 char length) and some contains only numbers (variable length 3-8).

4. Although some of the csv files did not have start_station_name, start_station_id, end_station_name, end_station_id; these rows contain latitude and longitude data. This can be used to fill these empty values.

5. member_casual column contains 2 types of membership data: member or casual.

# Step 3: Processing Data (Cleaning and Transformation)
## Tools Used
* SQL (sqlite, DB Browser): To process and clean data for further analysis

* R: To analyze and visualize data

## Cleaning and Transformation of Data
1. All of the last 12 month's ride data has been separated month-wise in the server. For proper management all of the data chunks are combined in a single table named "cyclistic_trip_data"

2. COUNT() function was run to check the row count of the aggregated data-set. There are 5757551 rows in this data-set.

  
```
SELECT
  COUNT(*)
FROM
  cyclistic_trip_data
```
<img src="Screenshots/Screenshot 2025-04-29 232435.png" width="300">
<img src="Screenshots/Screenshot 2025-04-29 232443.png" width="300">

3. Since GPS (latitude and longitude) data can have similar fractional data of same location, this has been verified and transformed into average values and exported into csv file (avg_start_station, avg_end_station) and imported as avg_start_station and avg_end_station tables in the database for easier management of location data.
```

-- Checking for multiple GPS values of same location for start_station_name

SELECT
    start_station_name, 
    start_lat, 
    count(*)
FROM 
    cyclistic_trip_data
WHERE
    start_station_name is not NULL
GROUP BY
    start_station_name, start_lat;
```
<img src="Screenshots/Screenshot 2025-04-29 235851.png" width="600">
<img src="Screenshots/Screenshot 2025-04-29 235905.png" width="400">

Above mentioned procedure has been executed for the end_station_name column as well.

```

-- Calculating average GPS values for start_station_name

SELECT
    start_station_name,
    start_staion_id,
    average(start_lat) AS start_lat_avg,
    average(start_lng) AS start_lng_avg,
FROM 
    cyclistic_trip_data
WHERE
    start_station_name is not NULL
GROUP BY
    start_station_name
```
Result obtained from this query was saved as a csv file (avg_start_station_gps.csv and avg_end_station_gps.csv) for later usage as table and join with the rest of the trip data.

4. There has been some discrepancies regarding ride duration. Some of the ride durations came out negative (83 rows) and these were left out in the final cleaning query.
<img src="Screenshots/Screenshot 2025-04-30 000137.png" width="600">
<img src="Screenshots/Screenshot 2025-04-30 000150.png" width="400">
   Moreover, since there are full-day passes for casual riders, there has been 4198 entries of rides more than 24 hour duration and these were kept in the final      processed data set.
   
<img src="Screenshots/Screenshot 2025-04-30 000825.png" width="600">
<img src="Screenshots/Screenshot 2025-04-30 000838.png" width="400">

5. The previously collected trip data has been inner joined with avg_start_station and avg_end_station location data and exported to csv file for analysis using following SQL query:

  

