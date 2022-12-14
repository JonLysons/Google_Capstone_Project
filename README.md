# Google Capstone Project

## Introduction
The final step in the Google Data Analytics Course is the Capstone Project. Here, you have a choice of two assignments. I chose the bike-share case study.

Using the data analysis steps proscribed by the course, here is my solution and methodology.

### Table of Contents
- [Step 1: Ask](#step-1-ask)
- [Step 2: Prepare](#step-2-prepare)
- [Step 3: Process](step-3-process)
- [Step 4: Analyse](#step-4-analyse)
- [Step 5: Share](#step-5-share)
- [Step 6: Act](#step-6-act)

## Step 1: Ask

The first step in the process is the Ask stage. The project starts off by asking questions. This is to help define the problem. 

### Background

In 2016, Cyclistic launched a successful bike-share offering. Since then, the programme has grown to a fleet of 5,824 bicycles that are geotracked and locked into a network of 692 stations across Chicago in the US.

Cyclistic’s marketing strategy has used general awareness to appeal to broad consumer segments. To do this Cyclistic used flexible pricing plans: single-ride passes, full-day passes and annual memberships. Single-ride or full-day passes are referred to as casual riders, while annual memberships are called members.

### Business Task

Cyclistic’s finance analysts have found that annual members are much more profitable than casual riders. Although the pricing flexibility helps the company to attract more customers, maximizing the number of annual members will be key to future growth. Rather than creating a marketing campaign that targets all-new customers, the company wants to convert casual riders into members.

### Key Stakeholder

The key stakeholder in this project is Lily Moreno, director of marketing. Moreno is responsible for the development of campaigns and initiatives to promote the bike-share programme.

### Objective

Moreno has set a clear goal: design marketing strategies aimed at converting casual riders into annual members. To do that, the marketing analyst team needs to understand the differences between how annual members and casual riders use its service, why casual riders would buy a membership, and how digital media could affect their marketing tactics. Moreno and her team are interested in analyzing the Cyclistic historical bike trip data to identify trends.

Moreno has identified three questions will guide the future marketing programme:
1. How do annual members and casual riders use Cyclistic bikes differently?
2. Why would casual riders buy Cyclistic annual memberships?
3. How can Cyclistic use digital media to influence casual riders to become members?

And I have been assigned the first question: how do annual members and casual riders use Cyclistic bikes differently?

Finding a data-driven answer to this question will help Moreno decide upon her marketing tactics. 

## Step 2: Prepare

The next stage is Prepare. This involves collecting and storing the information. 

### Method

I am to use the company's historical trip data to analyse and identify trends over the preceding 12 months. The data for this project can be downloaded from [here](https://divvy-tripdata.s3.amazonaws.com/index.html) in a zip format, with each file containing the data for one calendar month. I selected and downloaded data from August 2021 to July 2022. Unzipping the files, the data was contained in .csv files.

A good data source is ROCCC which stands for Reliable, Original, Comprehensive, Current and Cited.

**Reliable** – HIGH, this is first-party data that has been collected by Cyclistic.

**Original** – HIGH, the data is original.

**Comprehensive** – MEDIUM, some spreadsheets were missing data, but enough on the usage of casual and member riders for the purposses of this query.

**Current** – HIGH, I chose the most recent 12 months so the data is current.

**Cited** – HIGH, because the data originates from Cyclistic, it has a vetted source so is credible.

Overall, the dataset is considered good quality data, giving an accuate look at past usage of the bike-share scheme in Chicago over the previous 12 months. It is worth noting that certain information has been removed to address privacy concerns by protecting user identity and from linking to credit card numbers. This means that we won’t be able to connect pass purchases to credit card numbers to determine if casual riders live in the Cyclistic service area or if they have purchased multiple single passes.

The data has a high degree of integrity as it has been collated by Cyclistic. Analysing this data will help to answer the question assigned to me by finding out whether there are any differences or not in how the two types of bike riders use the service.

Potential problems are the size of the files, which vary from 19MB to 153MB – larger files might become unweildly in Google Sheets. If this happens then I might switch to Excel and if that fail then I'll just jump straight into RStudio.  

Looking at these in more detail, it seems there is a pattern. For the months from May to October (summer-autumn) the file sizes are much larger. For November to April (winter-spring), the file sizes are smaller. This is something worth exploring because if the file size correlates to the amount of data, then less data in the colder months may point to fewer bike rides.

This creates an interesting hypothesis to examine: namely are casual riders seasonal and member riders all-year round?

To make the data naming more user-friendly, I change the file names from `202207-divvy-tripdata.csv` to `2022_07_TripData.csv`.

## Step 3: Process

Process data by cleaning and checking the information.

### Method

As expected, the spreadsheets proved to be too unwieldly for Google Sheets, but I had much better luck in Excel, which opened them easily. First glance at the data revealed that there are 13 columns with close to 700,000 rows. As mentioned above, I also noticed the different file sizes.

The 13 column heads are:
`ride_id` `rideable_type` `started_at` `ended_at` `start_station_name` `start_station_id` `end_station_name` `end_station_id` `start_lat` `start_lng` `end_lat` `end_lng` `member_casual`

Briefly looking at the data in each column, it is apparent that most of the missing data is confined to four columns `start_station_name`  `start_station_id`  `end_station_name`  `end_station_id`. It also looks at if some of this data is in different formats. I decided to replace the missing cells with null, because data in other columns for these entries could still be useful. Reminder, I'm looking to compare the data for Casual and Member riders.

#### The Cleaing process

1. Removed a few duplicate entries in the `ride_id` column using the `Filter` function.
2. Removed some `ride_id` that had become corrupted, again using the `Filter` function. These were `ride_id` that had significantly more or less than 16 characters.
3. Replaced empty cells with _null_ using Find and Replace. There were mainly for `start_station_name` `start_station_id` `end_station_name` `end_station_id`.
4. The `started_at` and `ended_at` columns contained both the date and time, so I split these off into separate cells, so I created four new columns under the headings  `start_date`  `start_time`  `end_date`  `end_time`. I wanted to create another column for ride duration but Excel started to run slowly, so I do this in R Studio.
5. I left the `start_station_name` `start_station_id` `end_station_name` `end_station_id` `start_lat` `start_lng` `end_lat` `end_lng` for the moment. With more time available, I could resolve some of the issues by using the `start_lat` `start_lng` `end_lat` `end_lng` to find out the station names and station ids but that would possibly lose sight of the question that I'm trying to answer, namely "How do annual members and casual riders use Cyclistic bikes differently?"
6. Timmed some white spaces. 
7. Added another column for the day of the week. 
8. Saved the cleaned datasets in a new file as `.csv`.

## Step 4: Analyse

Analyse data to find patterns, relationships, and trends.

Decided to use RStudio.

### Method

First, I installed some packages
`install.packages("tidyverse")`
`install.packages("skimr")`
`install.packages("janitor")`

Then loaded specific tools `library(tidyverse)`, `library(lubridate)`, `library(dplyr)`, `ibrary(readr)`, `library(readxl)`, `library(skimr)` and `library(janitor)`.

Imported the 12 `.CSV` files into R Studio and renamed them in RStudio:

`Rides_08_2021 <- read_csv("desktop/Capstone_Data/6_Cleaned_Data/2021_08_TripData.csv")`

Used `ls()` to make sure all datasets were uploaded and used `str(Rides_08_2021)` to summarise the dataset.

Used `rbind` to combine the datasets into one file for analysis.

`BikeRides <- rbind(Rides_08_2021, Rides_09_2021, Rides_10_2021, Rides_11_2021, Rides_12_2021, Rides_01_2022, Rides_02_2022, Rides_03_2022, Rides_04_2022, Rides_05_2022, Rides_06_2022, Rides_07_2022)`

This produced a dataset with almost 6 million rows.

Changed the format of the cells so that I could do some calculations

```BikeRides3 <- BikeRides2 %>%
  mutate(end_date = ymd(end_date)) %>%
  mutate(start_date = ymd(start_date)) %>%
  mutate(started_at = as.POSIXct(started_at)) %>%
  mutate(ended_at = as.POSIXct(ended_at))
  ```
  
Added a new column for `ride_duration`, `weekday` and `month`and filled with data
 
`BikeRides3$ride_duration <- difftime(BikeRides3$ended_at, BikeRides3$started_at, units="mins")` added a new column and calculated the duration of the ride
  
`BikeRides3$weekday <- wday(BikeRides3$start_date, label = TRUE, abbr=FALSE, week_start = getOption("lubridate.week.start", 1))` added a new column with the day of the week

`BikeRides3$month <- month(BikeRides3$start_date, label = TRUE, abbr = FALSE)` added a new column with the month

Worked out the number of casual to member riders

```BikeRides3 %>%
  group_by(member_casual) %>%
  count(member_casual)
```

|  member_casual | number |
| --- | --- |
| casual | 2,522,226 |
| member | 3,379,237 |

Worked out the mean ride times for both casual and member riders (includes `round` to limit to two decimal places

```BikeRides3 %>%
  group_by(member_casual) %>%
  summarise(mean_ride_time = round(mean(ride_duration), 2))
```

| member_casual | mean_ride_time |
| --- | --- |
| casual | 29.21 mins |
| member | 12.93 mins |

This suggests that casual riders spend longer riding the bike than those with memberships.

Then counted the number of member and casual riders per weekday

```BikeRides3 %>%
  group_by(member_casual) %>%
  count(weekday)
```

| member_casual | weekday | number
| --- | --- | --- |
| casual | Monday | 299,656 |
| casual | Tuesday | 273,826 |
| casual | Wednesday | 281,783 |
| casual | Thursday | 316,118 |
| casual | Friday | 347,642 |
| casual | Saturday | 527,575 |
| casual | Sunday | 475,626 |
| member | Monday | 472,392 |
| member | Tuesday | 523,387 |
| member | Wednesday | 522,648 |
| member | Thursday | 522,662 |
| member | Friday | 466,680 |
| member | Saturday | 453,490 |
| member | Sunday | 417,978 |

It appears that member riders are more regular users, while casual riders peak at weekends. But it would be better displayed as a barchart

Next did the same thing for the months

```BikeRides3 %>%
  group_by(member_casual) %>%
  count(month)
```

| member_casual | month |  number
| --- | --- | --- |
| casual | January | 18,520 |
| casual | February | 21,416 |
| casual | March | 89,882 |
| casual | April | 126,417 |
| casual | May | 280,415 |
| casual | June | 369,051 |
| casual | July | 406,055 |
| casual | August | 412,671 |
| casual | September | 363,890 |
| casual | October | 257,242 |
| casual | November | 106,929 |
| casual | December | 69,738 |
| member | January | 85,250 |
| member | February | 94,193 |
| member | March | 194,160 |
| member | April | 244,832 |
| member | May | 354,443 |
| member | June | 400,153 |
| member | July | 417,433 |
| member | August | 391,681 |
| member | September | 392,257 |
| member | October | 373,984 |
| member | November | 253,049 |
| member | December | 177,802 |

It seems from this that usage is seasonal, summer months are more popular. There was too much missing data from the start and end locations to be able to draw any meaninful conclusion.

## Step 5: Share

Share data with your audience.

### Method

I created several charts to illustrate the differences between the Casual and Member users.

First, I compared Casual and Member users

```
ggplot(data = BikeRides3) + 
  geom_bar(mapping = aes(x = member_casual, fill = member_casual, width = 0.5)) +
  labs(title = "Casual vs Member riders", x = "Type of User", y = "Number of Users") +
  scale_fill_brewer(palette = "Set1") +
  scale_y_continuous(breaks = c(0, 500000, 1000000, 1500000, 2000000, 2500000, 3000000, 3500000)) +
  theme(legend.position="none")
```
![UserTypes](https://user-images.githubusercontent.com/117950069/207711957-ba06343d-7022-4578-a1da-8dd28c65650d.png)

While Members make up the majority of users with 57.2% of total users, this leaves 42.8% Casual users who can be converted into Members and thus grow the scheme. 

Next, I compared the Casual and Member usage over the course of the week

```
ggplot(data = rides_week) + 
  (aes(x = weekday, y= number, fill = member_casual, width = 0.75)) +
  geom_col(position = "dodge") +
  labs(title = "Number of Users on Each Day", x = "Type of User", y = "Number of Users") +
  scale_fill_brewer(palette = "Set1") +
  scale_y_continuous(breaks = c(0, 50000, 100000, 150000, 200000, 250000, 300000, 350000, 400000, 450000, 500000)) +
  theme(axis.text.x = element_text(angle = 60, hjust =1), legend.position="none")
```

![RidesWeek](https://user-images.githubusercontent.com/117950069/207713796-c66aadc6-4784-4d72-a160-8cf18d5b5aff.png)

From this chart, it appears that the Member usage is fairly consistent over the course of the week, marginally tapering off during the weekend. But for the Casual rider, usage increases significantly at the weekend.

And finally, I compared the Casual and Member usage for each month over the course of the 12 month sample. 

```
ggplot(data = rides_month) + 
  (aes(x = month, y= number, fill = member_casual, width = 0.75)) +
  geom_col(position = "dodge") +
  labs(title = "Number of Monthly Riders ", x = "Month", y = "Number of Users") +
  scale_fill_brewer(palette = "Set1") +
  scale_y_continuous(breaks = c(0, 50000, 100000, 150000, 200000, 250000, 300000, 350000, 400000, 450000)) +
  theme(axis.text.x = element_text(angle = 60, hjust =1), legend.position="none")
```

![RidesMonth](https://user-images.githubusercontent.com/117950069/207713860-72b421a1-14ea-41fd-99b8-c1938d279a3d.png)

At suggested by the files sizes at the start of this project, the winter months saw a fall in usage with both January and February being the lowest for both Casual and Member riders. For Members, usage steadily increases from March onwards, peaking in July and holding steady until falling in November. For Casual riders, there is a sharp increase in May for the summer months, peaking in August. There then is sharp decline in Casual usage in November as winter sets in.

## Step 6: Act

Act on the data and use the analysis results.

### Method

With this data, I have several recommendations for Moreno as a way to convert Casual users into members. 

1. Start a marketing campaign in March to attract Casual users to the scheme so that they can make the most of their memberships during the peak usage during the summer months.
2. Explore different types of membership schemes, with perhaps a six-month membership that covers the summer months as another way of attracting casual users onto the memberhip roster.
3. Introduce a new annual membership plan that just covers weekend users. Again, this would be targetted at Casual users and would be another way of converting Casual users into members. 
4. Do further research to find out whether Casual users live in the Chicago area or are from other locations as this would enable more targetted advertising campaign. This could result in short-term membership plans for Casual users that don't live in the Chicago area. 
5. Re-examine the data gathering techniques to ensure that data for the start and end locations is more complete for future analysis. More complete data in this area would allow better examination of the location of users, which may provide insight into the best locations for advertising campaigns to inform Casual users about the different membership options. 

Overall, I enjoyed this project. The Excel part was relatively simple and quick to complete due to existing knowledge. But I particularly enjoyed using RStudio. Working out the little bits of script to process and analyse the data was a lot of fun, and I'm looking forward to using R more in the future.
The downsides, I didn't really get a chance to use Tableau since I used R to create the charts, so I'll do some Tableau specific projects in the future. And I didn't get the chance to use SQL, so again I'll look at some dedicated SQL projects to do in the future. 
