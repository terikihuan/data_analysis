﻿# Bellabeat Case Study

This case study is a capstone project for the Google Data Analytics Professional Certificate on Coursera. For this case study, I analyze smart devices data to gain insight into how customers are using their devices and present my findings to stakeholders. I will be following Google 6 steps of Data Analysis, which are Ask, Prepare, Process, Analyze, Share and Act.

# About Bellabeat

Bellabeat is a company that makes smart health and fitness technology for women. Founded in 2014 by Urška Sršen and Sandro Mur, Bellabeat aims to help women make informed decisions about their health and wellness every day. Bellabeat’s products include wearable devices that track biometric and lifestyle data, such as heart rate, respiratory rate, sleep quality, menstrual cycle, activity, and stress. Bellabeat also offers a subscription service that provides personalized coaching, guidance, and content in various wellness segments, such as nutrition, mindfulness, exercise, and sex. Bellabeat’s app syncs with its devices and gives users insights into their health and wellness based on their natural cycle. Bellabeat’s products are designed and engineered for women, with a feminine and elegant look that can match any style. Bellabeat has been endorsed by celebrities and influencers such as Olivia Culpo, Amanda Seyfried, Chiara Ferragni, and Kourtney Kardashian.

# Analysis

Below is my analysis for the case study. There are 6 steps to the analysis: Ask, Prepare, Process, Analyze, Share and Act.

## Ask


**Business task:**
Analyze the data from Fitbit's devices to gain insight into how customers are using smart devices to inform Bellabeat marketing strategy.

**Question for analysis:**

 1. What are some trends in smart device usage?
 2. How could these trends apply to Bellabeat customers?
 3. How could these trends help influence Bellabeat marketing strategy?

**Key stakeholders**

 - **Urška Sršen**: Bellabeat’s cofounder and Chief Creative Officer
 - **Sando Mur**: Mathematician and Bellabeat’s cofounder; key member of the Bellabeat executive team
 - **Bellabeat marketing analytics team**: A team of data analysts responsible for collecting, analyzing, and reporting data that helps guide Bellabeat’s marketing strategy

## Prepare

**Data source:** [FitBit Fitness Tracker Data | Kaggle](https://www.kaggle.com/datasets/arashnic/fitbit)
This Kaggle data set contains personal fitness tracker from thirty Fitbit users. Thirty eligible Fitbit users consented to the submission of personal tracker data, including minute-level output for physical activity, heart rate, and sleep monitoring. It includes information about daily activity, steps, and heart rate that can be used to explore users’ habits. The dataset is generated by respondents to a distributed survey via Amazon Mechanical Turk between 03.12.2016-05.12.2016.

The data is stored in CSV format and has in total 18 different files in long format.

**ROCCC Analysis**
- **Reliability**: Low, because of the low sample size (33 participants)
- **Originality**: Low, third-party public dataset via Amazon Mechanical Turk
- **Comprehensiveness**: Medium, dataset contains many information such as daily activities, sleep durations, metabolic rate, calories burnt, etc. However, data about participants like genders, age or location are not included.
- **Current**: Low, as of the time of writing, the data is 7 years old. There might be some cultural shift or change in people lifestyle within this time period.
- **Cited**: High, the data and author are well-documented on Kaggle.

**Data selection**:

This analysis will use the daily activity data since they will provide the high-level information about participants physical activities. The following files in the dataset will be used:

- dailyActivity_merge.csv
- sleepDay_merged.csv

## Process

This analysis will use R studio to process, analyze and visualize the data. The reason is that R provide the flexibility to customize my analysis process.

First, install and load all necessary packages for analysis.
```
install.packages("tidyverse")
install.packages("here")
install.packages("skimr")
install.packages("janitor")
install.packages("dplyr")

library("tidyverse")
library("here")
library("skimr")
library("janitor")
library("dplyr")
```
We then import the csv files and read them as data frame.
```
daily_activity <- read_csv("dailyActivity_merged.csv")
sleep_day <- read_csv("sleepDay_merged.csv")
```
We can use n_distinct() to see the unique participant in each of the files.
```
n_distinct(daily_activity$Id)
[1] 33
n_distinct(sleep_day$Id)
[1] 24
```
As we can see, the Daily Activity data has 33 unique participants, while the Sleep day data only has 24.


## Analyze

This analysis uses summary() to get the statistical summary of the Daily activity data.
```
daily_activity %>% 
  select(TotalSteps,
         TotalDistance,
         VeryActiveMinutes,
         FairlyActiveMinutes,
         LightlyActiveMinutes,
         SedentaryMinutes,
         Calories) %>% 
  summary()
```
```
 TotalSteps    TotalDistance    VeryActiveMinutes FairlyActiveMinutes
 Min.   :    0   Min.   : 0.000   Min.   :  0.00    Min.   :  0.00     
 1st Qu.: 3790   1st Qu.: 2.620   1st Qu.:  0.00    1st Qu.:  0.00     
 Median : 7406   Median : 5.245   Median :  4.00    Median :  6.00     
 Mean   : 7638   Mean   : 5.490   Mean   : 21.16    Mean   : 13.56     
 3rd Qu.:10727   3rd Qu.: 7.713   3rd Qu.: 32.00    3rd Qu.: 19.00     
 Max.   :36019   Max.   :28.030   Max.   :210.00    Max.   :143.00     
 LightlyActiveMinutes SedentaryMinutes    Calories   
 Min.   :  0.0        Min.   :   0.0   Min.   :   0  
 1st Qu.:127.0        1st Qu.: 729.8   1st Qu.:1828  
 Median :199.0        Median :1057.5   Median :2134  
 Mean   :192.8        Mean   : 991.2   Mean   :2304  
 3rd Qu.:264.0        3rd Qu.:1229.5   3rd Qu.:2793  
 Max.   :518.0        Max.   :1440.0   Max.   :4900
```
**Observations:**

 - The average steps walked is 7638, while the average distance walked is 5.49 km. 
 - Active times are classified into 3 types: very active, fairly active and lightly active; the respective times for each type are 21.16, 13.56 and 192.8 minutes.
 - The average sedentary time is 991 minutes.
 - The average daily calories burnt is 2304 kcal.

Here is a summary for the sleep data.
```
sleep_day %>% 
  select(TotalSleepRecords,
         TotalMinutesAsleep,
         TotalTimeInBed) %>% 
  summary()
```
```
 TotalSleepRecords TotalMinutesAsleep TotalTimeInBed 
 Min.   :1.000     Min.   : 58.0      Min.   : 61.0  
 1st Qu.:1.000     1st Qu.:361.0      1st Qu.:403.0  
 Median :1.000     Median :433.0      Median :463.0  
 Mean   :1.119     Mean   :419.5      Mean   :458.6  
 3rd Qu.:1.000     3rd Qu.:490.0      3rd Qu.:526.0  
 Max.   :3.000     Max.   :796.0      Max.   :961.0
```
**Observation:**

- The majority sleeps once per day.
- Average time spent sleeping is 419.5 minutes (almost 7 hours).
- Average time in bed is a bit longer, 458.6 minutes or 7.64 hours.

## Share

We will look at the relationship between total number of steps and calories burned.
```
geom_point(mapping=aes(x=TotalSteps, y=Calories), color="red") +
  geom_smooth(mapping=aes(x=TotalSteps, y=Calories)) +
  labs(title="The Relationship Between Total Steps and Calories", x="Total Steps", y="Calories Burned (kcal)")
```
![Steps and Calories graph](images/steps_kcal.png)

The graph shows that there is a positive correlation between total number of steps and calories burned. The higher the step counts, the more calories burned.

Next, we look at the relationship between very active minutes, fairly active minutes, slightly active minutes and calories burned.

```
ggplot(data=daily_activity) + 
  geom_point(mapping=aes(x=VeryActiveMinutes, y=Calories), color="orange") +
  geom_smooth(mapping=aes(x=VeryActiveMinutes, y=Calories)) +
  labs(title="The Relationship Between Very Active Minutes and Calories", x="Very Active Minutes", y="Calories Burned (kcal)")
```

![Very Active Minutes and Calories graph](images/veryActive_kcal.png)

```
ggplot(data=daily_activity) + 
  geom_point(mapping=aes(x=FairlyActiveMinutes, y=Calories), color="orange") +
  geom_smooth(mapping=aes(x=FairlyActiveMinutes, y=Calories)) +
  labs(title="The Relationship Between Failry Active Minutes and Calories", x="Failry Active Minutes", y="Calories Burned (kcal)")
```
![Fairly Active Minutes and Calories graph](images/fairlyActive_kcal.png)
```
ggplot(data=daily_activity) + 
  geom_point(mapping=aes(x=LightlyActiveMinutes, y=Calories), color="orange") +
  geom_smooth(mapping=aes(x=LightlyActiveMinutes, y=Calories)) +
  labs(title="The Relationship Between Lightly Active Minutes and Calories", x="Lightly Active Minutes", y="Calories Burned (kcal)")
```
![Lightly Active Minutes and Calories graph](images/lightlyActive_kcal.png)

The graphs show that Very Active Minutes are positively correlated with calories burned. But Lightly Active Minutes can burn more calories per day, possibly due to it having longer duration than Very Active Minutes. As for Fairly Active Minutes, there are hardly any correlation with calories burned.

Lastly, we look at the relationship between Total Distance and Calories burned.
```
ggplot(data=daily_activity) + 
  geom_smooth(mapping=aes(x=TotalDistance, y=Calories)) +
  labs(title="The Relationship Between Total Distance and Calories", x="Total Distance", y="Calories Burned (kcal)")
```
![Distance and Calories graph](images/distance_kcal.png)

We can clearly see that the longer the distance walked, the more calories burned.

## Act

**Recommendation:**

- Based on the findings, more time spending exercising, more step counts and more distance translate to more calories burned. We can encourage user to exercise more through reminders. 

- The majority still lead a sedentary lifestyle. We can promote a more active lifestyle (especially the very active) through campaigns and events on social media.

- While users on average achieve 7600 steps per day, this is still far from the optimal 10000 steps recommended. We can regularly remind user to meet this goal.

- Remind user to be active if they have been sedentary for an extended period of time.





