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

  

