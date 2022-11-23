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

Potential problems are the size of the files, which vary from 19MB to 153MB – larger files might become unweildly in Google Sheets. If this happens then I might switch to R Studio.   

To make the data naming more user-friendly, I change the file names from `202207-divvy-tripdata.csv` to `2022_07_TripData.csv`.

## Step 3: Process

Process data by cleaning and checking the information.

### Method

## Step 4: Analyse

Analyse data to find patterns, relationships, and trends.

### Method

## Step 5: Share

Share data with your audience.

### Method

## Step 6: Act

Act on the data and use the analysis results.

### Method
