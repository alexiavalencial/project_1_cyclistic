# Project 1: Cyclistic

This is a project I did for my Data Analytics Course by Google, where I analyzed data from the company records and built a recommendation to convert casual customers to annual membership customers.

## Introduction

The bicycle rental sector has grown exponentially in recent years, due to its economic, social, and environmental benefits. However, they have also had to face various challenges, such as the declining economy and keeping their audience with them, preventing them from going with the competition or using other types of transportation.

**Scenario**

This practical case is based on a fictitious company called “Cyclistic”, which offers a bicycle rental service in Chicago, United States. Its mission is to provide a more economical, healthy, and sustainable transportation alternative for citizens.

Cyclistic has flexible pricing plans to meet consumer needs. Customers who obtain a single trip or daily pass are considered **casual** customers, while those who opt for annual memberships are considered **members**.

The marketing director believes that the future success of the company depends on getting casual customers to acquire memberships, thus increasing the number of annual members.
To support business decisions, it is necessary to analyze data from the last 12 months.

The question that will guide this analysis will be the following:
How are annual members and casual cyclists different regarding using Cyclistic bikes?

The following tools were used to answer this question: spreadsheets to clean and analyze the monthly data, and Tableau to visualize the results obtained.

The analysis focused on the variables related to user preference (duration, frequency, and day of trips), making a distinction between casual customers and members.

**Data Source**

The historical data used for the analysis corresponds to a period of 12 months, from December 1, 2022, to November 30, 2023. This data was provided by Motivate International Inc., a bicycle rental company located in the city of Chicago, United States. It contains information about the trips made by users, including the month, day, and time the trip started and ended, as well as the type of bicycle used.

The data is available for free download and can be consulted in the following "[link to the data source](https://divvy-tripdata.s3.amazonaws.com/index.html)”, under this “[link to the license agreement](https://divvybikes.com/data-license-agreement)”.

**Data Credibility**

The data source was classified as reliable because it comes from a primary source. The company that provides the service is responsible for collecting the data and storing it for later analysis.

## Prepare data for analysis**

It was necessary to convert the files from .csv to .xlsx to run the analysis in the spreadsheet program.

**Identify the structure of the data**

Data distribution format:
- Each file corresponded to a month, each of them consisted of 13 columns and the number of rows varied depending on the trips made in said month.
Trip details:
- The ride_id column contains unique identifiers for each ride.
- The rideable_type column indicates what type of bicycle was used on each trip.
- The started_at and ended_at columns record the start and end date and time of each trip.
Station information:
- The start_station_name and end_station_name columns contain the names of the start and end stations, respectively. However, it is observed that some of these cells are empty, suggesting that information is not available for all stations.
- The columns start_station_id and end_station_id contain station identifiers, and it is also observed that some cells are empty.
Geospatial information:
- The start_lat, start_lng, end_lat, and end_lng columns contain latitude and longitude data for the start and end locations of each trip.
Type of user:
- The column member_casual records the type of user who took each trip, with values such as “Member” and “Casual”.

## Data processing

To keep the data separated by month, it was decided to do an individual analysis for each file.

**Data Cleaning**

The following precautions were taken to clean and prepare the data for analysis:

1. The “rideable_type” columns were filtered to validate that there were only valid values (classic_bike, docked_bike, electric_bike) and the “member_casual” column to corroborate, in the same way, that there are only two types of entries (member and casual). Those rows where any of this data was empty were eliminated to avoid any bias or margin of error.
2. The started_at and ended_at columns were converted to the same date (yyyy-mm-dd) and time (hh:mm:ss) format.

**Add specific information**

Seven new columns with basic metrics were added to facilitate the identification of trends and patterns in travel:

1. ride_length: To calculate the duration of the trips, the operation of subtracting the “ended_at” column from “started_at” was performed.
- It was decided to eliminate those trips with a duration of 0 seconds and negative values to avoid information that did not add value or affect the analysis.
2. Day of week: the formula “=WEEKDAY(C:C,1)” was applied to record the day of the week on which said trip was executed, where 1 is equivalent to Sunday and 7 to Saturday.
3. # of trips: the formula “=COUNT(O:O)” was used to determine the total number of trips made, as well as the formulas “=COUNTIF(M:M,"MEMBER")” and “=COUNTIF(M: M,"casual")” to determine how many of those trips were taken by members and casual customers.
4. avg_ride_length: This column added the average length of total trips, as well as trips taken by members and casual customers. The formulas used in this column were: “=AVERAGE(N:N)”, “=AVERAGEIF(M:M, "member",N:N)” and “=AVERAGEIF(M:M,"casual", N: N)” respectively.
5. Most_common_day: “=MODE(O:O)” was used to find the day of the week with the most total trips. A small table was also added to count the number of trips made per day and segment by the type of customer (member or casual), this was carried out using the formula “=COUNTIFS”.
6. Members% and casual%: in this pair of columns a division was made between the number of clients according to their type and the total number of trips made, to have a clearer idea of the percentage that each type of client represents.
7. Another small table was added using the same “=COUNTIFS” formula, to count the type of bicycle used by both types of clients.
8. Finally, a pivot table was added in a different sheet (Avg ride_length p/d), with the average trip duration according to the day and type of customer.
All of these analyses helped us better understand user behaviors depending on the day and type of customer.

## Data frame analysis.

**All data**

A [spreadsheet](https://docs.google.com/spreadsheets/u/0/d/1quTg1X3cOns02grdMN5VZNOeJ9SAv6CPP98zO5htOTo/edit) was specifically designated to establish a data set including all the columns created in the twelve files analyzed, to facilitate access and analysis by detecting trends.

From this data, we can see that in twelve months, 5,677,524 travel data were collected. It is observed that Tuesday was the day with the most trips recorded throughout the year. The average duration of the trips was approximately 16 minutes and 21 seconds. However, there are extremely high values, an example is a trip found of 560 hours with 03 minutes and 44 seconds, and other trips with a duration of 01 or 02 seconds, which could be considered atypical. 

**Comparison of trip duration statistics between “Members” and “Casual” users**

Of the total trips collected, 3,625,154 (67.47%) were users with annual memberships and 2,052,370 (32.53%) were casual customers.

Average duration:
Members: 12 minutes and 01 seconds.
Casual: 25 minutes and 52 seconds.

This indicates that, on average, casual users have significantly longer trips compared to member users. The average trip duration for occasional users has increased by 96%.

Most frequent day of the week:
Members: 3 (Tuesday).
Casual: 7 (Saturday).

In casual clients, a slight preference for weekends was observed. Unlike member customers, who usually use the service on weekdays.

Average duration per day:

Using the results of pivot tables, a significant increase in the duration of trips on weekends was detected for both users, with a notable peak on Saturdays.

## Data visualization

A graph was made to represent the number of total trips and number of trips by members and casual users.

![Monthly_trips (1)](https://github.com/alexiavalencial/data_analytics_portfolio/assets/153674734/2b14dfb5-eafb-4845-8ee0-5925c3717d99)

With these findings, we can identify that trips tend to increase during the summer and decrease considerably as temperatures decrease. The blue bars represent the total trips per month, regardless of the type of user. In turn, it was decided to give a representation in the same graph of the number of trips for each type of user. We noticed that the number of members is noticeably greater than the number of casual customers, although we also noticed an increase in casual customers during the summer season.

The percentage ratio of members and casuals remains relatively stable during the winter months, with a constant approximate ratio of 25-30% to 70-75%, with annual members being above. See the graph where the percentage of casual users is represented in the orange bars and the percentage of members in the line above them.

![Members_casuals %](https://github.com/alexiavalencial/data_analytics_portfolio/assets/153674734/9bff1b88-0a6e-4f03-af69-61a5dcbcade8)

However, we can notice how this changes during the summer months, as this gap begins to close considerably, due to the increase in casual customers and the decrease in annual members.

**Most frequent day of the week**

Below, the findings are presented considering the days with the most trip records according to the type of customer. Where 1=“Sunday” and 7=“Saturday”.

![Common_Day_of_week](https://github.com/alexiavalencial/data_analytics_portfolio/assets/153674734/e710894d-a7a0-4060-b78d-ba850013017d)

**Trip duration**

The following graph represents the average duration of the trips, classifying them according to the type of user.

![Average Ride Lenght (1)](https://github.com/alexiavalencial/data_analytics_portfolio/assets/153674734/b7ede8fc-0fe1-4da5-93e6-11eaca99d663)

Based on these graphs, we can summarize that:

Casual users:
- They tend to use the service commonly on Saturdays or Sundays, especially in summer.
The average duration of their trips are usually longer, with August being the month with the longest duration (35 minutes and 15 seconds) and November with the shortest duration (19 minutes and 26 seconds).
- The number of casual users increases considerably in June, July, and August.

Users with membership:
- They usually use the service during weekdays (Monday to Friday), with Tuesday being the most frequent day.
- The average duration of their trips is usually less than 15 minutes, with August being the longest (13 minutes and 46 seconds) and January being the shortest (10 minutes and 22 seconds).
- The number of members using the service decreased in June, July, and August, with July having the lowest number of members. Of a total of 767,650, only 436,292 (56.83%) were members. But this number recovered from November to March, with January having the highest percentage of Members (78.97%).

In both cases, weekends are the days with the longest average trip duration.

These graphs are available in Tableau Public and can be consulted using the following link.

[Practical Case: Cyclistic](https://public.tableau.com/views/CasoPrcticoCyclistic/Monthly_trips?:language=es-ES&:display_count=n&:origin=viz_share_link)

## Conclusion

The increase in casual customers and the decrease in annual members during the summer could be because casual members are customers who go to Chicago for the summer and tend to use the service for recreational use, unlike annual members. , who, judging by the use during the week and the duration per trip, tend to use it for some specific purpose, either to go to work or school, which would explain why in summer the use of members decreases.

It was also observed that the high atypical trip duration values corresponded, for the most part, to casual users, so it would be necessary to analyze the reason why these members see it as more convenient to keep the bicycle for a long time. On the contrary, low outliers are more frequent in member users. With the current information and findings, it was not possible to determine whether the outliers represent valid data or errors in the records, and to provide a more reliable analysis, it would be necessary to define whether the outliers are accurate or if they are errors.
Historical data from previous years would be required to confirm if the trends found in these months are an annual pattern or if it was an isolated event that external factors are causing.

In summary, given that the company's objective is to convert casual users into annual members, the strategies recommended to the Marketing team would be:

1. Create two marketing campaigns, one focused on those casual users who consider themselves local users, and another on non-local customers, since users who use the service sporadically or who are visiting the city are unlikely to opt to purchase an annual membership.
2. For non-local users, special packages aimed at visitors to the city (tourists and/or foreigners) could be implemented and public acceptance subsequently measured.
3. A Marketing campaign on social networks, mentioning the benefits of the bicycle as a means of transportation compared to other methods, focusing on the money and time that can be saved, the distances that can be covered in a few minutes, and the views that can be enjoyed while traveling from point A to point B, making it sound attractive to both casual users and potential customers.
