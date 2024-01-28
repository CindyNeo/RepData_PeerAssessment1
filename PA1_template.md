---
title: "Reproducible Research: Peer Assessment 1"
output: 
  html_document:
    keep_md: true
---

## Setting Global Options


```r
library(knitr)
```

```
## Warning: package 'knitr' was built under R version 4.2.3
```

```r
opts_chunk$set(echo = TRUE, results = 'asis', warning = FALSE)
```

## 1. Loading and preprocessing the data

### 1.1 Check if the directory exists


```r
if (!file.exists("Dataset")) {
    dir.create("Dataset")
}
```

### 1.2 Download the data into directory


```r
Url = "https://d396qusza40orc.cloudfront.net/repdata%2Fdata%2Factivity.zip"
download.file(Url, destfile = "./Dataset/stepsData.zip")
```

### 1.3 Unzip the dataset


```r
unzip(zipfile = "./Dataset/stepsData.zip", 
      exdir = "./Dataset")
```

### 1.4 Load the data into R


```r
activity <- read.csv("./Dataset/activity.csv")
library(xtable)
head <- xtable(head(activity))
print(head, type = "html")
```

<!-- html table generated in R 4.2.2 by xtable 1.8-4 package -->
<!-- Sun Jan 28 20:56:39 2024 -->
<table border=1>
<tr> <th>  </th> <th> steps </th> <th> date </th> <th> interval </th>  </tr>
  <tr> <td align="right"> 1 </td> <td align="right">  </td> <td> 2012-10-01 </td> <td align="right">   0 </td> </tr>
  <tr> <td align="right"> 2 </td> <td align="right">  </td> <td> 2012-10-01 </td> <td align="right">   5 </td> </tr>
  <tr> <td align="right"> 3 </td> <td align="right">  </td> <td> 2012-10-01 </td> <td align="right">  10 </td> </tr>
  <tr> <td align="right"> 4 </td> <td align="right">  </td> <td> 2012-10-01 </td> <td align="right">  15 </td> </tr>
  <tr> <td align="right"> 5 </td> <td align="right">  </td> <td> 2012-10-01 </td> <td align="right">  20 </td> </tr>
  <tr> <td align="right"> 6 </td> <td align="right">  </td> <td> 2012-10-01 </td> <td align="right">  25 </td> </tr>
   </table>

## 2. What is mean total number of steps taken per day?

### 2.1 Calculate the total number of steps taken per day


```r
total_steps_per_day <- with(activity, aggregate(steps, by = list(date), sum, na.rm = TRUE))

total_steps_per_day <- xtable(total_steps_per_day)
print(total_steps_per_day, type = "html")
```

<!-- html table generated in R 4.2.2 by xtable 1.8-4 package -->
<!-- Sun Jan 28 20:56:39 2024 -->
<table border=1>
<tr> <th>  </th> <th> Group.1 </th> <th> x </th>  </tr>
  <tr> <td align="right"> 1 </td> <td> 2012-10-01 </td> <td align="right">   0 </td> </tr>
  <tr> <td align="right"> 2 </td> <td> 2012-10-02 </td> <td align="right"> 126 </td> </tr>
  <tr> <td align="right"> 3 </td> <td> 2012-10-03 </td> <td align="right"> 11352 </td> </tr>
  <tr> <td align="right"> 4 </td> <td> 2012-10-04 </td> <td align="right"> 12116 </td> </tr>
  <tr> <td align="right"> 5 </td> <td> 2012-10-05 </td> <td align="right"> 13294 </td> </tr>
  <tr> <td align="right"> 6 </td> <td> 2012-10-06 </td> <td align="right"> 15420 </td> </tr>
  <tr> <td align="right"> 7 </td> <td> 2012-10-07 </td> <td align="right"> 11015 </td> </tr>
  <tr> <td align="right"> 8 </td> <td> 2012-10-08 </td> <td align="right">   0 </td> </tr>
  <tr> <td align="right"> 9 </td> <td> 2012-10-09 </td> <td align="right"> 12811 </td> </tr>
  <tr> <td align="right"> 10 </td> <td> 2012-10-10 </td> <td align="right"> 9900 </td> </tr>
  <tr> <td align="right"> 11 </td> <td> 2012-10-11 </td> <td align="right"> 10304 </td> </tr>
  <tr> <td align="right"> 12 </td> <td> 2012-10-12 </td> <td align="right"> 17382 </td> </tr>
  <tr> <td align="right"> 13 </td> <td> 2012-10-13 </td> <td align="right"> 12426 </td> </tr>
  <tr> <td align="right"> 14 </td> <td> 2012-10-14 </td> <td align="right"> 15098 </td> </tr>
  <tr> <td align="right"> 15 </td> <td> 2012-10-15 </td> <td align="right"> 10139 </td> </tr>
  <tr> <td align="right"> 16 </td> <td> 2012-10-16 </td> <td align="right"> 15084 </td> </tr>
  <tr> <td align="right"> 17 </td> <td> 2012-10-17 </td> <td align="right"> 13452 </td> </tr>
  <tr> <td align="right"> 18 </td> <td> 2012-10-18 </td> <td align="right"> 10056 </td> </tr>
  <tr> <td align="right"> 19 </td> <td> 2012-10-19 </td> <td align="right"> 11829 </td> </tr>
  <tr> <td align="right"> 20 </td> <td> 2012-10-20 </td> <td align="right"> 10395 </td> </tr>
  <tr> <td align="right"> 21 </td> <td> 2012-10-21 </td> <td align="right"> 8821 </td> </tr>
  <tr> <td align="right"> 22 </td> <td> 2012-10-22 </td> <td align="right"> 13460 </td> </tr>
  <tr> <td align="right"> 23 </td> <td> 2012-10-23 </td> <td align="right"> 8918 </td> </tr>
  <tr> <td align="right"> 24 </td> <td> 2012-10-24 </td> <td align="right"> 8355 </td> </tr>
  <tr> <td align="right"> 25 </td> <td> 2012-10-25 </td> <td align="right"> 2492 </td> </tr>
  <tr> <td align="right"> 26 </td> <td> 2012-10-26 </td> <td align="right"> 6778 </td> </tr>
  <tr> <td align="right"> 27 </td> <td> 2012-10-27 </td> <td align="right"> 10119 </td> </tr>
  <tr> <td align="right"> 28 </td> <td> 2012-10-28 </td> <td align="right"> 11458 </td> </tr>
  <tr> <td align="right"> 29 </td> <td> 2012-10-29 </td> <td align="right"> 5018 </td> </tr>
  <tr> <td align="right"> 30 </td> <td> 2012-10-30 </td> <td align="right"> 9819 </td> </tr>
  <tr> <td align="right"> 31 </td> <td> 2012-10-31 </td> <td align="right"> 15414 </td> </tr>
  <tr> <td align="right"> 32 </td> <td> 2012-11-01 </td> <td align="right">   0 </td> </tr>
  <tr> <td align="right"> 33 </td> <td> 2012-11-02 </td> <td align="right"> 10600 </td> </tr>
  <tr> <td align="right"> 34 </td> <td> 2012-11-03 </td> <td align="right"> 10571 </td> </tr>
  <tr> <td align="right"> 35 </td> <td> 2012-11-04 </td> <td align="right">   0 </td> </tr>
  <tr> <td align="right"> 36 </td> <td> 2012-11-05 </td> <td align="right"> 10439 </td> </tr>
  <tr> <td align="right"> 37 </td> <td> 2012-11-06 </td> <td align="right"> 8334 </td> </tr>
  <tr> <td align="right"> 38 </td> <td> 2012-11-07 </td> <td align="right"> 12883 </td> </tr>
  <tr> <td align="right"> 39 </td> <td> 2012-11-08 </td> <td align="right"> 3219 </td> </tr>
  <tr> <td align="right"> 40 </td> <td> 2012-11-09 </td> <td align="right">   0 </td> </tr>
  <tr> <td align="right"> 41 </td> <td> 2012-11-10 </td> <td align="right">   0 </td> </tr>
  <tr> <td align="right"> 42 </td> <td> 2012-11-11 </td> <td align="right"> 12608 </td> </tr>
  <tr> <td align="right"> 43 </td> <td> 2012-11-12 </td> <td align="right"> 10765 </td> </tr>
  <tr> <td align="right"> 44 </td> <td> 2012-11-13 </td> <td align="right"> 7336 </td> </tr>
  <tr> <td align="right"> 45 </td> <td> 2012-11-14 </td> <td align="right">   0 </td> </tr>
  <tr> <td align="right"> 46 </td> <td> 2012-11-15 </td> <td align="right">  41 </td> </tr>
  <tr> <td align="right"> 47 </td> <td> 2012-11-16 </td> <td align="right"> 5441 </td> </tr>
  <tr> <td align="right"> 48 </td> <td> 2012-11-17 </td> <td align="right"> 14339 </td> </tr>
  <tr> <td align="right"> 49 </td> <td> 2012-11-18 </td> <td align="right"> 15110 </td> </tr>
  <tr> <td align="right"> 50 </td> <td> 2012-11-19 </td> <td align="right"> 8841 </td> </tr>
  <tr> <td align="right"> 51 </td> <td> 2012-11-20 </td> <td align="right"> 4472 </td> </tr>
  <tr> <td align="right"> 52 </td> <td> 2012-11-21 </td> <td align="right"> 12787 </td> </tr>
  <tr> <td align="right"> 53 </td> <td> 2012-11-22 </td> <td align="right"> 20427 </td> </tr>
  <tr> <td align="right"> 54 </td> <td> 2012-11-23 </td> <td align="right"> 21194 </td> </tr>
  <tr> <td align="right"> 55 </td> <td> 2012-11-24 </td> <td align="right"> 14478 </td> </tr>
  <tr> <td align="right"> 56 </td> <td> 2012-11-25 </td> <td align="right"> 11834 </td> </tr>
  <tr> <td align="right"> 57 </td> <td> 2012-11-26 </td> <td align="right"> 11162 </td> </tr>
  <tr> <td align="right"> 58 </td> <td> 2012-11-27 </td> <td align="right"> 13646 </td> </tr>
  <tr> <td align="right"> 59 </td> <td> 2012-11-28 </td> <td align="right"> 10183 </td> </tr>
  <tr> <td align="right"> 60 </td> <td> 2012-11-29 </td> <td align="right"> 7047 </td> </tr>
  <tr> <td align="right"> 61 </td> <td> 2012-11-30 </td> <td align="right">   0 </td> </tr>
   </table>

### 2.1.1 Changing the column names for total_steps_per_day


```r
names(total_steps_per_day) <- c("Date", "Steps")

total_steps_per_day <- xtable(total_steps_per_day)
print(total_steps_per_day, type = "html")
```

<!-- html table generated in R 4.2.2 by xtable 1.8-4 package -->
<!-- Sun Jan 28 20:56:39 2024 -->
<table border=1>
<tr> <th>  </th> <th> Date </th> <th> Steps </th>  </tr>
  <tr> <td align="right"> 1 </td> <td> 2012-10-01 </td> <td align="right">   0 </td> </tr>
  <tr> <td align="right"> 2 </td> <td> 2012-10-02 </td> <td align="right"> 126 </td> </tr>
  <tr> <td align="right"> 3 </td> <td> 2012-10-03 </td> <td align="right"> 11352 </td> </tr>
  <tr> <td align="right"> 4 </td> <td> 2012-10-04 </td> <td align="right"> 12116 </td> </tr>
  <tr> <td align="right"> 5 </td> <td> 2012-10-05 </td> <td align="right"> 13294 </td> </tr>
  <tr> <td align="right"> 6 </td> <td> 2012-10-06 </td> <td align="right"> 15420 </td> </tr>
  <tr> <td align="right"> 7 </td> <td> 2012-10-07 </td> <td align="right"> 11015 </td> </tr>
  <tr> <td align="right"> 8 </td> <td> 2012-10-08 </td> <td align="right">   0 </td> </tr>
  <tr> <td align="right"> 9 </td> <td> 2012-10-09 </td> <td align="right"> 12811 </td> </tr>
  <tr> <td align="right"> 10 </td> <td> 2012-10-10 </td> <td align="right"> 9900 </td> </tr>
  <tr> <td align="right"> 11 </td> <td> 2012-10-11 </td> <td align="right"> 10304 </td> </tr>
  <tr> <td align="right"> 12 </td> <td> 2012-10-12 </td> <td align="right"> 17382 </td> </tr>
  <tr> <td align="right"> 13 </td> <td> 2012-10-13 </td> <td align="right"> 12426 </td> </tr>
  <tr> <td align="right"> 14 </td> <td> 2012-10-14 </td> <td align="right"> 15098 </td> </tr>
  <tr> <td align="right"> 15 </td> <td> 2012-10-15 </td> <td align="right"> 10139 </td> </tr>
  <tr> <td align="right"> 16 </td> <td> 2012-10-16 </td> <td align="right"> 15084 </td> </tr>
  <tr> <td align="right"> 17 </td> <td> 2012-10-17 </td> <td align="right"> 13452 </td> </tr>
  <tr> <td align="right"> 18 </td> <td> 2012-10-18 </td> <td align="right"> 10056 </td> </tr>
  <tr> <td align="right"> 19 </td> <td> 2012-10-19 </td> <td align="right"> 11829 </td> </tr>
  <tr> <td align="right"> 20 </td> <td> 2012-10-20 </td> <td align="right"> 10395 </td> </tr>
  <tr> <td align="right"> 21 </td> <td> 2012-10-21 </td> <td align="right"> 8821 </td> </tr>
  <tr> <td align="right"> 22 </td> <td> 2012-10-22 </td> <td align="right"> 13460 </td> </tr>
  <tr> <td align="right"> 23 </td> <td> 2012-10-23 </td> <td align="right"> 8918 </td> </tr>
  <tr> <td align="right"> 24 </td> <td> 2012-10-24 </td> <td align="right"> 8355 </td> </tr>
  <tr> <td align="right"> 25 </td> <td> 2012-10-25 </td> <td align="right"> 2492 </td> </tr>
  <tr> <td align="right"> 26 </td> <td> 2012-10-26 </td> <td align="right"> 6778 </td> </tr>
  <tr> <td align="right"> 27 </td> <td> 2012-10-27 </td> <td align="right"> 10119 </td> </tr>
  <tr> <td align="right"> 28 </td> <td> 2012-10-28 </td> <td align="right"> 11458 </td> </tr>
  <tr> <td align="right"> 29 </td> <td> 2012-10-29 </td> <td align="right"> 5018 </td> </tr>
  <tr> <td align="right"> 30 </td> <td> 2012-10-30 </td> <td align="right"> 9819 </td> </tr>
  <tr> <td align="right"> 31 </td> <td> 2012-10-31 </td> <td align="right"> 15414 </td> </tr>
  <tr> <td align="right"> 32 </td> <td> 2012-11-01 </td> <td align="right">   0 </td> </tr>
  <tr> <td align="right"> 33 </td> <td> 2012-11-02 </td> <td align="right"> 10600 </td> </tr>
  <tr> <td align="right"> 34 </td> <td> 2012-11-03 </td> <td align="right"> 10571 </td> </tr>
  <tr> <td align="right"> 35 </td> <td> 2012-11-04 </td> <td align="right">   0 </td> </tr>
  <tr> <td align="right"> 36 </td> <td> 2012-11-05 </td> <td align="right"> 10439 </td> </tr>
  <tr> <td align="right"> 37 </td> <td> 2012-11-06 </td> <td align="right"> 8334 </td> </tr>
  <tr> <td align="right"> 38 </td> <td> 2012-11-07 </td> <td align="right"> 12883 </td> </tr>
  <tr> <td align="right"> 39 </td> <td> 2012-11-08 </td> <td align="right"> 3219 </td> </tr>
  <tr> <td align="right"> 40 </td> <td> 2012-11-09 </td> <td align="right">   0 </td> </tr>
  <tr> <td align="right"> 41 </td> <td> 2012-11-10 </td> <td align="right">   0 </td> </tr>
  <tr> <td align="right"> 42 </td> <td> 2012-11-11 </td> <td align="right"> 12608 </td> </tr>
  <tr> <td align="right"> 43 </td> <td> 2012-11-12 </td> <td align="right"> 10765 </td> </tr>
  <tr> <td align="right"> 44 </td> <td> 2012-11-13 </td> <td align="right"> 7336 </td> </tr>
  <tr> <td align="right"> 45 </td> <td> 2012-11-14 </td> <td align="right">   0 </td> </tr>
  <tr> <td align="right"> 46 </td> <td> 2012-11-15 </td> <td align="right">  41 </td> </tr>
  <tr> <td align="right"> 47 </td> <td> 2012-11-16 </td> <td align="right"> 5441 </td> </tr>
  <tr> <td align="right"> 48 </td> <td> 2012-11-17 </td> <td align="right"> 14339 </td> </tr>
  <tr> <td align="right"> 49 </td> <td> 2012-11-18 </td> <td align="right"> 15110 </td> </tr>
  <tr> <td align="right"> 50 </td> <td> 2012-11-19 </td> <td align="right"> 8841 </td> </tr>
  <tr> <td align="right"> 51 </td> <td> 2012-11-20 </td> <td align="right"> 4472 </td> </tr>
  <tr> <td align="right"> 52 </td> <td> 2012-11-21 </td> <td align="right"> 12787 </td> </tr>
  <tr> <td align="right"> 53 </td> <td> 2012-11-22 </td> <td align="right"> 20427 </td> </tr>
  <tr> <td align="right"> 54 </td> <td> 2012-11-23 </td> <td align="right"> 21194 </td> </tr>
  <tr> <td align="right"> 55 </td> <td> 2012-11-24 </td> <td align="right"> 14478 </td> </tr>
  <tr> <td align="right"> 56 </td> <td> 2012-11-25 </td> <td align="right"> 11834 </td> </tr>
  <tr> <td align="right"> 57 </td> <td> 2012-11-26 </td> <td align="right"> 11162 </td> </tr>
  <tr> <td align="right"> 58 </td> <td> 2012-11-27 </td> <td align="right"> 13646 </td> </tr>
  <tr> <td align="right"> 59 </td> <td> 2012-11-28 </td> <td align="right"> 10183 </td> </tr>
  <tr> <td align="right"> 60 </td> <td> 2012-11-29 </td> <td align="right"> 7047 </td> </tr>
  <tr> <td align="right"> 61 </td> <td> 2012-11-30 </td> <td align="right">   0 </td> </tr>
   </table>

### 2.2 Make a histogram of the total number of steps taken each day


```r
hist(total_steps_per_day$Steps,
     main = "Histogram of the total number of steps taken each day",
     xlab = "Total number of steps taken each day")
```

![](PA1_template_files/figure-html/histogram-1.png)<!-- -->

### 2.3 Calculate and report the mean and median of the total number of steps taken per day

The mean of the total number of steps taken per day is:


```r
mean(total_steps_per_day$Steps)
```

[1] 9354.23

The median of the total number of steps taken per day is:


```r
median(total_steps_per_day$Steps)
```

[1] 10395

## 3. What is the average daily activity pattern?

### 3.1 Make a time series plot (i.e. type = "l") of the 5-minute interval (x-axis) and the average number of steps taken, averaged across all days (y-axis)


```r
average_steps_per_interval <- with(activity, aggregate(steps, by = list(interval), mean, na.rm = TRUE))

average_steps_per_interval <- xtable(average_steps_per_interval)
print(average_steps_per_interval, type = "html")
```

<!-- html table generated in R 4.2.2 by xtable 1.8-4 package -->
<!-- Sun Jan 28 20:56:39 2024 -->
<table border=1>
<tr> <th>  </th> <th> Group.1 </th> <th> x </th>  </tr>
  <tr> <td align="right"> 1 </td> <td align="right">   0 </td> <td align="right"> 1.72 </td> </tr>
  <tr> <td align="right"> 2 </td> <td align="right">   5 </td> <td align="right"> 0.34 </td> </tr>
  <tr> <td align="right"> 3 </td> <td align="right">  10 </td> <td align="right"> 0.13 </td> </tr>
  <tr> <td align="right"> 4 </td> <td align="right">  15 </td> <td align="right"> 0.15 </td> </tr>
  <tr> <td align="right"> 5 </td> <td align="right">  20 </td> <td align="right"> 0.08 </td> </tr>
  <tr> <td align="right"> 6 </td> <td align="right">  25 </td> <td align="right"> 2.09 </td> </tr>
  <tr> <td align="right"> 7 </td> <td align="right">  30 </td> <td align="right"> 0.53 </td> </tr>
  <tr> <td align="right"> 8 </td> <td align="right">  35 </td> <td align="right"> 0.87 </td> </tr>
  <tr> <td align="right"> 9 </td> <td align="right">  40 </td> <td align="right"> 0.00 </td> </tr>
  <tr> <td align="right"> 10 </td> <td align="right">  45 </td> <td align="right"> 1.47 </td> </tr>
  <tr> <td align="right"> 11 </td> <td align="right">  50 </td> <td align="right"> 0.30 </td> </tr>
  <tr> <td align="right"> 12 </td> <td align="right">  55 </td> <td align="right"> 0.13 </td> </tr>
  <tr> <td align="right"> 13 </td> <td align="right"> 100 </td> <td align="right"> 0.32 </td> </tr>
  <tr> <td align="right"> 14 </td> <td align="right"> 105 </td> <td align="right"> 0.68 </td> </tr>
  <tr> <td align="right"> 15 </td> <td align="right"> 110 </td> <td align="right"> 0.15 </td> </tr>
  <tr> <td align="right"> 16 </td> <td align="right"> 115 </td> <td align="right"> 0.34 </td> </tr>
  <tr> <td align="right"> 17 </td> <td align="right"> 120 </td> <td align="right"> 0.00 </td> </tr>
  <tr> <td align="right"> 18 </td> <td align="right"> 125 </td> <td align="right"> 1.11 </td> </tr>
  <tr> <td align="right"> 19 </td> <td align="right"> 130 </td> <td align="right"> 1.83 </td> </tr>
  <tr> <td align="right"> 20 </td> <td align="right"> 135 </td> <td align="right"> 0.17 </td> </tr>
  <tr> <td align="right"> 21 </td> <td align="right"> 140 </td> <td align="right"> 0.17 </td> </tr>
  <tr> <td align="right"> 22 </td> <td align="right"> 145 </td> <td align="right"> 0.38 </td> </tr>
  <tr> <td align="right"> 23 </td> <td align="right"> 150 </td> <td align="right"> 0.26 </td> </tr>
  <tr> <td align="right"> 24 </td> <td align="right"> 155 </td> <td align="right"> 0.00 </td> </tr>
  <tr> <td align="right"> 25 </td> <td align="right"> 200 </td> <td align="right"> 0.00 </td> </tr>
  <tr> <td align="right"> 26 </td> <td align="right"> 205 </td> <td align="right"> 0.00 </td> </tr>
  <tr> <td align="right"> 27 </td> <td align="right"> 210 </td> <td align="right"> 1.13 </td> </tr>
  <tr> <td align="right"> 28 </td> <td align="right"> 215 </td> <td align="right"> 0.00 </td> </tr>
  <tr> <td align="right"> 29 </td> <td align="right"> 220 </td> <td align="right"> 0.00 </td> </tr>
  <tr> <td align="right"> 30 </td> <td align="right"> 225 </td> <td align="right"> 0.13 </td> </tr>
  <tr> <td align="right"> 31 </td> <td align="right"> 230 </td> <td align="right"> 0.00 </td> </tr>
  <tr> <td align="right"> 32 </td> <td align="right"> 235 </td> <td align="right"> 0.23 </td> </tr>
  <tr> <td align="right"> 33 </td> <td align="right"> 240 </td> <td align="right"> 0.00 </td> </tr>
  <tr> <td align="right"> 34 </td> <td align="right"> 245 </td> <td align="right"> 0.00 </td> </tr>
  <tr> <td align="right"> 35 </td> <td align="right"> 250 </td> <td align="right"> 1.55 </td> </tr>
  <tr> <td align="right"> 36 </td> <td align="right"> 255 </td> <td align="right"> 0.94 </td> </tr>
  <tr> <td align="right"> 37 </td> <td align="right"> 300 </td> <td align="right"> 0.00 </td> </tr>
  <tr> <td align="right"> 38 </td> <td align="right"> 305 </td> <td align="right"> 0.00 </td> </tr>
  <tr> <td align="right"> 39 </td> <td align="right"> 310 </td> <td align="right"> 0.00 </td> </tr>
  <tr> <td align="right"> 40 </td> <td align="right"> 315 </td> <td align="right"> 0.00 </td> </tr>
  <tr> <td align="right"> 41 </td> <td align="right"> 320 </td> <td align="right"> 0.21 </td> </tr>
  <tr> <td align="right"> 42 </td> <td align="right"> 325 </td> <td align="right"> 0.62 </td> </tr>
  <tr> <td align="right"> 43 </td> <td align="right"> 330 </td> <td align="right"> 1.62 </td> </tr>
  <tr> <td align="right"> 44 </td> <td align="right"> 335 </td> <td align="right"> 0.58 </td> </tr>
  <tr> <td align="right"> 45 </td> <td align="right"> 340 </td> <td align="right"> 0.49 </td> </tr>
  <tr> <td align="right"> 46 </td> <td align="right"> 345 </td> <td align="right"> 0.08 </td> </tr>
  <tr> <td align="right"> 47 </td> <td align="right"> 350 </td> <td align="right"> 0.00 </td> </tr>
  <tr> <td align="right"> 48 </td> <td align="right"> 355 </td> <td align="right"> 0.00 </td> </tr>
  <tr> <td align="right"> 49 </td> <td align="right"> 400 </td> <td align="right"> 1.19 </td> </tr>
  <tr> <td align="right"> 50 </td> <td align="right"> 405 </td> <td align="right"> 0.94 </td> </tr>
  <tr> <td align="right"> 51 </td> <td align="right"> 410 </td> <td align="right"> 2.57 </td> </tr>
  <tr> <td align="right"> 52 </td> <td align="right"> 415 </td> <td align="right"> 0.00 </td> </tr>
  <tr> <td align="right"> 53 </td> <td align="right"> 420 </td> <td align="right"> 0.34 </td> </tr>
  <tr> <td align="right"> 54 </td> <td align="right"> 425 </td> <td align="right"> 0.36 </td> </tr>
  <tr> <td align="right"> 55 </td> <td align="right"> 430 </td> <td align="right"> 4.11 </td> </tr>
  <tr> <td align="right"> 56 </td> <td align="right"> 435 </td> <td align="right"> 0.66 </td> </tr>
  <tr> <td align="right"> 57 </td> <td align="right"> 440 </td> <td align="right"> 3.49 </td> </tr>
  <tr> <td align="right"> 58 </td> <td align="right"> 445 </td> <td align="right"> 0.83 </td> </tr>
  <tr> <td align="right"> 59 </td> <td align="right"> 450 </td> <td align="right"> 3.11 </td> </tr>
  <tr> <td align="right"> 60 </td> <td align="right"> 455 </td> <td align="right"> 1.11 </td> </tr>
  <tr> <td align="right"> 61 </td> <td align="right"> 500 </td> <td align="right"> 0.00 </td> </tr>
  <tr> <td align="right"> 62 </td> <td align="right"> 505 </td> <td align="right"> 1.57 </td> </tr>
  <tr> <td align="right"> 63 </td> <td align="right"> 510 </td> <td align="right"> 3.00 </td> </tr>
  <tr> <td align="right"> 64 </td> <td align="right"> 515 </td> <td align="right"> 2.25 </td> </tr>
  <tr> <td align="right"> 65 </td> <td align="right"> 520 </td> <td align="right"> 3.32 </td> </tr>
  <tr> <td align="right"> 66 </td> <td align="right"> 525 </td> <td align="right"> 2.96 </td> </tr>
  <tr> <td align="right"> 67 </td> <td align="right"> 530 </td> <td align="right"> 2.09 </td> </tr>
  <tr> <td align="right"> 68 </td> <td align="right"> 535 </td> <td align="right"> 6.06 </td> </tr>
  <tr> <td align="right"> 69 </td> <td align="right"> 540 </td> <td align="right"> 16.02 </td> </tr>
  <tr> <td align="right"> 70 </td> <td align="right"> 545 </td> <td align="right"> 18.34 </td> </tr>
  <tr> <td align="right"> 71 </td> <td align="right"> 550 </td> <td align="right"> 39.45 </td> </tr>
  <tr> <td align="right"> 72 </td> <td align="right"> 555 </td> <td align="right"> 44.49 </td> </tr>
  <tr> <td align="right"> 73 </td> <td align="right"> 600 </td> <td align="right"> 31.49 </td> </tr>
  <tr> <td align="right"> 74 </td> <td align="right"> 605 </td> <td align="right"> 49.26 </td> </tr>
  <tr> <td align="right"> 75 </td> <td align="right"> 610 </td> <td align="right"> 53.77 </td> </tr>
  <tr> <td align="right"> 76 </td> <td align="right"> 615 </td> <td align="right"> 63.45 </td> </tr>
  <tr> <td align="right"> 77 </td> <td align="right"> 620 </td> <td align="right"> 49.96 </td> </tr>
  <tr> <td align="right"> 78 </td> <td align="right"> 625 </td> <td align="right"> 47.08 </td> </tr>
  <tr> <td align="right"> 79 </td> <td align="right"> 630 </td> <td align="right"> 52.15 </td> </tr>
  <tr> <td align="right"> 80 </td> <td align="right"> 635 </td> <td align="right"> 39.34 </td> </tr>
  <tr> <td align="right"> 81 </td> <td align="right"> 640 </td> <td align="right"> 44.02 </td> </tr>
  <tr> <td align="right"> 82 </td> <td align="right"> 645 </td> <td align="right"> 44.17 </td> </tr>
  <tr> <td align="right"> 83 </td> <td align="right"> 650 </td> <td align="right"> 37.36 </td> </tr>
  <tr> <td align="right"> 84 </td> <td align="right"> 655 </td> <td align="right"> 49.04 </td> </tr>
  <tr> <td align="right"> 85 </td> <td align="right"> 700 </td> <td align="right"> 43.81 </td> </tr>
  <tr> <td align="right"> 86 </td> <td align="right"> 705 </td> <td align="right"> 44.38 </td> </tr>
  <tr> <td align="right"> 87 </td> <td align="right"> 710 </td> <td align="right"> 50.51 </td> </tr>
  <tr> <td align="right"> 88 </td> <td align="right"> 715 </td> <td align="right"> 54.51 </td> </tr>
  <tr> <td align="right"> 89 </td> <td align="right"> 720 </td> <td align="right"> 49.92 </td> </tr>
  <tr> <td align="right"> 90 </td> <td align="right"> 725 </td> <td align="right"> 50.98 </td> </tr>
  <tr> <td align="right"> 91 </td> <td align="right"> 730 </td> <td align="right"> 55.68 </td> </tr>
  <tr> <td align="right"> 92 </td> <td align="right"> 735 </td> <td align="right"> 44.32 </td> </tr>
  <tr> <td align="right"> 93 </td> <td align="right"> 740 </td> <td align="right"> 52.26 </td> </tr>
  <tr> <td align="right"> 94 </td> <td align="right"> 745 </td> <td align="right"> 69.55 </td> </tr>
  <tr> <td align="right"> 95 </td> <td align="right"> 750 </td> <td align="right"> 57.85 </td> </tr>
  <tr> <td align="right"> 96 </td> <td align="right"> 755 </td> <td align="right"> 56.15 </td> </tr>
  <tr> <td align="right"> 97 </td> <td align="right"> 800 </td> <td align="right"> 73.38 </td> </tr>
  <tr> <td align="right"> 98 </td> <td align="right"> 805 </td> <td align="right"> 68.21 </td> </tr>
  <tr> <td align="right"> 99 </td> <td align="right"> 810 </td> <td align="right"> 129.43 </td> </tr>
  <tr> <td align="right"> 100 </td> <td align="right"> 815 </td> <td align="right"> 157.53 </td> </tr>
  <tr> <td align="right"> 101 </td> <td align="right"> 820 </td> <td align="right"> 171.15 </td> </tr>
  <tr> <td align="right"> 102 </td> <td align="right"> 825 </td> <td align="right"> 155.40 </td> </tr>
  <tr> <td align="right"> 103 </td> <td align="right"> 830 </td> <td align="right"> 177.30 </td> </tr>
  <tr> <td align="right"> 104 </td> <td align="right"> 835 </td> <td align="right"> 206.17 </td> </tr>
  <tr> <td align="right"> 105 </td> <td align="right"> 840 </td> <td align="right"> 195.92 </td> </tr>
  <tr> <td align="right"> 106 </td> <td align="right"> 845 </td> <td align="right"> 179.57 </td> </tr>
  <tr> <td align="right"> 107 </td> <td align="right"> 850 </td> <td align="right"> 183.40 </td> </tr>
  <tr> <td align="right"> 108 </td> <td align="right"> 855 </td> <td align="right"> 167.02 </td> </tr>
  <tr> <td align="right"> 109 </td> <td align="right"> 900 </td> <td align="right"> 143.45 </td> </tr>
  <tr> <td align="right"> 110 </td> <td align="right"> 905 </td> <td align="right"> 124.04 </td> </tr>
  <tr> <td align="right"> 111 </td> <td align="right"> 910 </td> <td align="right"> 109.11 </td> </tr>
  <tr> <td align="right"> 112 </td> <td align="right"> 915 </td> <td align="right"> 108.11 </td> </tr>
  <tr> <td align="right"> 113 </td> <td align="right"> 920 </td> <td align="right"> 103.72 </td> </tr>
  <tr> <td align="right"> 114 </td> <td align="right"> 925 </td> <td align="right"> 95.96 </td> </tr>
  <tr> <td align="right"> 115 </td> <td align="right"> 930 </td> <td align="right"> 66.21 </td> </tr>
  <tr> <td align="right"> 116 </td> <td align="right"> 935 </td> <td align="right"> 45.23 </td> </tr>
  <tr> <td align="right"> 117 </td> <td align="right"> 940 </td> <td align="right"> 24.79 </td> </tr>
  <tr> <td align="right"> 118 </td> <td align="right"> 945 </td> <td align="right"> 38.75 </td> </tr>
  <tr> <td align="right"> 119 </td> <td align="right"> 950 </td> <td align="right"> 34.98 </td> </tr>
  <tr> <td align="right"> 120 </td> <td align="right"> 955 </td> <td align="right"> 21.06 </td> </tr>
  <tr> <td align="right"> 121 </td> <td align="right"> 1000 </td> <td align="right"> 40.57 </td> </tr>
  <tr> <td align="right"> 122 </td> <td align="right"> 1005 </td> <td align="right"> 26.98 </td> </tr>
  <tr> <td align="right"> 123 </td> <td align="right"> 1010 </td> <td align="right"> 42.42 </td> </tr>
  <tr> <td align="right"> 124 </td> <td align="right"> 1015 </td> <td align="right"> 52.66 </td> </tr>
  <tr> <td align="right"> 125 </td> <td align="right"> 1020 </td> <td align="right"> 38.92 </td> </tr>
  <tr> <td align="right"> 126 </td> <td align="right"> 1025 </td> <td align="right"> 50.79 </td> </tr>
  <tr> <td align="right"> 127 </td> <td align="right"> 1030 </td> <td align="right"> 44.28 </td> </tr>
  <tr> <td align="right"> 128 </td> <td align="right"> 1035 </td> <td align="right"> 37.42 </td> </tr>
  <tr> <td align="right"> 129 </td> <td align="right"> 1040 </td> <td align="right"> 34.70 </td> </tr>
  <tr> <td align="right"> 130 </td> <td align="right"> 1045 </td> <td align="right"> 28.34 </td> </tr>
  <tr> <td align="right"> 131 </td> <td align="right"> 1050 </td> <td align="right"> 25.09 </td> </tr>
  <tr> <td align="right"> 132 </td> <td align="right"> 1055 </td> <td align="right"> 31.94 </td> </tr>
  <tr> <td align="right"> 133 </td> <td align="right"> 1100 </td> <td align="right"> 31.36 </td> </tr>
  <tr> <td align="right"> 134 </td> <td align="right"> 1105 </td> <td align="right"> 29.68 </td> </tr>
  <tr> <td align="right"> 135 </td> <td align="right"> 1110 </td> <td align="right"> 21.32 </td> </tr>
  <tr> <td align="right"> 136 </td> <td align="right"> 1115 </td> <td align="right"> 25.55 </td> </tr>
  <tr> <td align="right"> 137 </td> <td align="right"> 1120 </td> <td align="right"> 28.38 </td> </tr>
  <tr> <td align="right"> 138 </td> <td align="right"> 1125 </td> <td align="right"> 26.47 </td> </tr>
  <tr> <td align="right"> 139 </td> <td align="right"> 1130 </td> <td align="right"> 33.43 </td> </tr>
  <tr> <td align="right"> 140 </td> <td align="right"> 1135 </td> <td align="right"> 49.98 </td> </tr>
  <tr> <td align="right"> 141 </td> <td align="right"> 1140 </td> <td align="right"> 42.04 </td> </tr>
  <tr> <td align="right"> 142 </td> <td align="right"> 1145 </td> <td align="right"> 44.60 </td> </tr>
  <tr> <td align="right"> 143 </td> <td align="right"> 1150 </td> <td align="right"> 46.04 </td> </tr>
  <tr> <td align="right"> 144 </td> <td align="right"> 1155 </td> <td align="right"> 59.19 </td> </tr>
  <tr> <td align="right"> 145 </td> <td align="right"> 1200 </td> <td align="right"> 63.87 </td> </tr>
  <tr> <td align="right"> 146 </td> <td align="right"> 1205 </td> <td align="right"> 87.70 </td> </tr>
  <tr> <td align="right"> 147 </td> <td align="right"> 1210 </td> <td align="right"> 94.85 </td> </tr>
  <tr> <td align="right"> 148 </td> <td align="right"> 1215 </td> <td align="right"> 92.77 </td> </tr>
  <tr> <td align="right"> 149 </td> <td align="right"> 1220 </td> <td align="right"> 63.40 </td> </tr>
  <tr> <td align="right"> 150 </td> <td align="right"> 1225 </td> <td align="right"> 50.17 </td> </tr>
  <tr> <td align="right"> 151 </td> <td align="right"> 1230 </td> <td align="right"> 54.47 </td> </tr>
  <tr> <td align="right"> 152 </td> <td align="right"> 1235 </td> <td align="right"> 32.42 </td> </tr>
  <tr> <td align="right"> 153 </td> <td align="right"> 1240 </td> <td align="right"> 26.53 </td> </tr>
  <tr> <td align="right"> 154 </td> <td align="right"> 1245 </td> <td align="right"> 37.74 </td> </tr>
  <tr> <td align="right"> 155 </td> <td align="right"> 1250 </td> <td align="right"> 45.06 </td> </tr>
  <tr> <td align="right"> 156 </td> <td align="right"> 1255 </td> <td align="right"> 67.28 </td> </tr>
  <tr> <td align="right"> 157 </td> <td align="right"> 1300 </td> <td align="right"> 42.34 </td> </tr>
  <tr> <td align="right"> 158 </td> <td align="right"> 1305 </td> <td align="right"> 39.89 </td> </tr>
  <tr> <td align="right"> 159 </td> <td align="right"> 1310 </td> <td align="right"> 43.26 </td> </tr>
  <tr> <td align="right"> 160 </td> <td align="right"> 1315 </td> <td align="right"> 40.98 </td> </tr>
  <tr> <td align="right"> 161 </td> <td align="right"> 1320 </td> <td align="right"> 46.25 </td> </tr>
  <tr> <td align="right"> 162 </td> <td align="right"> 1325 </td> <td align="right"> 56.43 </td> </tr>
  <tr> <td align="right"> 163 </td> <td align="right"> 1330 </td> <td align="right"> 42.75 </td> </tr>
  <tr> <td align="right"> 164 </td> <td align="right"> 1335 </td> <td align="right"> 25.13 </td> </tr>
  <tr> <td align="right"> 165 </td> <td align="right"> 1340 </td> <td align="right"> 39.96 </td> </tr>
  <tr> <td align="right"> 166 </td> <td align="right"> 1345 </td> <td align="right"> 53.55 </td> </tr>
  <tr> <td align="right"> 167 </td> <td align="right"> 1350 </td> <td align="right"> 47.32 </td> </tr>
  <tr> <td align="right"> 168 </td> <td align="right"> 1355 </td> <td align="right"> 60.81 </td> </tr>
  <tr> <td align="right"> 169 </td> <td align="right"> 1400 </td> <td align="right"> 55.75 </td> </tr>
  <tr> <td align="right"> 170 </td> <td align="right"> 1405 </td> <td align="right"> 51.96 </td> </tr>
  <tr> <td align="right"> 171 </td> <td align="right"> 1410 </td> <td align="right"> 43.58 </td> </tr>
  <tr> <td align="right"> 172 </td> <td align="right"> 1415 </td> <td align="right"> 48.70 </td> </tr>
  <tr> <td align="right"> 173 </td> <td align="right"> 1420 </td> <td align="right"> 35.47 </td> </tr>
  <tr> <td align="right"> 174 </td> <td align="right"> 1425 </td> <td align="right"> 37.55 </td> </tr>
  <tr> <td align="right"> 175 </td> <td align="right"> 1430 </td> <td align="right"> 41.85 </td> </tr>
  <tr> <td align="right"> 176 </td> <td align="right"> 1435 </td> <td align="right"> 27.51 </td> </tr>
  <tr> <td align="right"> 177 </td> <td align="right"> 1440 </td> <td align="right"> 17.11 </td> </tr>
  <tr> <td align="right"> 178 </td> <td align="right"> 1445 </td> <td align="right"> 26.08 </td> </tr>
  <tr> <td align="right"> 179 </td> <td align="right"> 1450 </td> <td align="right"> 43.62 </td> </tr>
  <tr> <td align="right"> 180 </td> <td align="right"> 1455 </td> <td align="right"> 43.77 </td> </tr>
  <tr> <td align="right"> 181 </td> <td align="right"> 1500 </td> <td align="right"> 30.02 </td> </tr>
  <tr> <td align="right"> 182 </td> <td align="right"> 1505 </td> <td align="right"> 36.08 </td> </tr>
  <tr> <td align="right"> 183 </td> <td align="right"> 1510 </td> <td align="right"> 35.49 </td> </tr>
  <tr> <td align="right"> 184 </td> <td align="right"> 1515 </td> <td align="right"> 38.85 </td> </tr>
  <tr> <td align="right"> 185 </td> <td align="right"> 1520 </td> <td align="right"> 45.96 </td> </tr>
  <tr> <td align="right"> 186 </td> <td align="right"> 1525 </td> <td align="right"> 47.75 </td> </tr>
  <tr> <td align="right"> 187 </td> <td align="right"> 1530 </td> <td align="right"> 48.13 </td> </tr>
  <tr> <td align="right"> 188 </td> <td align="right"> 1535 </td> <td align="right"> 65.32 </td> </tr>
  <tr> <td align="right"> 189 </td> <td align="right"> 1540 </td> <td align="right"> 82.91 </td> </tr>
  <tr> <td align="right"> 190 </td> <td align="right"> 1545 </td> <td align="right"> 98.66 </td> </tr>
  <tr> <td align="right"> 191 </td> <td align="right"> 1550 </td> <td align="right"> 102.11 </td> </tr>
  <tr> <td align="right"> 192 </td> <td align="right"> 1555 </td> <td align="right"> 83.96 </td> </tr>
  <tr> <td align="right"> 193 </td> <td align="right"> 1600 </td> <td align="right"> 62.13 </td> </tr>
  <tr> <td align="right"> 194 </td> <td align="right"> 1605 </td> <td align="right"> 64.13 </td> </tr>
  <tr> <td align="right"> 195 </td> <td align="right"> 1610 </td> <td align="right"> 74.55 </td> </tr>
  <tr> <td align="right"> 196 </td> <td align="right"> 1615 </td> <td align="right"> 63.17 </td> </tr>
  <tr> <td align="right"> 197 </td> <td align="right"> 1620 </td> <td align="right"> 56.91 </td> </tr>
  <tr> <td align="right"> 198 </td> <td align="right"> 1625 </td> <td align="right"> 59.77 </td> </tr>
  <tr> <td align="right"> 199 </td> <td align="right"> 1630 </td> <td align="right"> 43.87 </td> </tr>
  <tr> <td align="right"> 200 </td> <td align="right"> 1635 </td> <td align="right"> 38.57 </td> </tr>
  <tr> <td align="right"> 201 </td> <td align="right"> 1640 </td> <td align="right"> 44.66 </td> </tr>
  <tr> <td align="right"> 202 </td> <td align="right"> 1645 </td> <td align="right"> 45.45 </td> </tr>
  <tr> <td align="right"> 203 </td> <td align="right"> 1650 </td> <td align="right"> 46.21 </td> </tr>
  <tr> <td align="right"> 204 </td> <td align="right"> 1655 </td> <td align="right"> 43.68 </td> </tr>
  <tr> <td align="right"> 205 </td> <td align="right"> 1700 </td> <td align="right"> 46.62 </td> </tr>
  <tr> <td align="right"> 206 </td> <td align="right"> 1705 </td> <td align="right"> 56.30 </td> </tr>
  <tr> <td align="right"> 207 </td> <td align="right"> 1710 </td> <td align="right"> 50.72 </td> </tr>
  <tr> <td align="right"> 208 </td> <td align="right"> 1715 </td> <td align="right"> 61.23 </td> </tr>
  <tr> <td align="right"> 209 </td> <td align="right"> 1720 </td> <td align="right"> 72.72 </td> </tr>
  <tr> <td align="right"> 210 </td> <td align="right"> 1725 </td> <td align="right"> 78.94 </td> </tr>
  <tr> <td align="right"> 211 </td> <td align="right"> 1730 </td> <td align="right"> 68.94 </td> </tr>
  <tr> <td align="right"> 212 </td> <td align="right"> 1735 </td> <td align="right"> 59.66 </td> </tr>
  <tr> <td align="right"> 213 </td> <td align="right"> 1740 </td> <td align="right"> 75.09 </td> </tr>
  <tr> <td align="right"> 214 </td> <td align="right"> 1745 </td> <td align="right"> 56.51 </td> </tr>
  <tr> <td align="right"> 215 </td> <td align="right"> 1750 </td> <td align="right"> 34.77 </td> </tr>
  <tr> <td align="right"> 216 </td> <td align="right"> 1755 </td> <td align="right"> 37.45 </td> </tr>
  <tr> <td align="right"> 217 </td> <td align="right"> 1800 </td> <td align="right"> 40.68 </td> </tr>
  <tr> <td align="right"> 218 </td> <td align="right"> 1805 </td> <td align="right"> 58.02 </td> </tr>
  <tr> <td align="right"> 219 </td> <td align="right"> 1810 </td> <td align="right"> 74.70 </td> </tr>
  <tr> <td align="right"> 220 </td> <td align="right"> 1815 </td> <td align="right"> 85.32 </td> </tr>
  <tr> <td align="right"> 221 </td> <td align="right"> 1820 </td> <td align="right"> 59.26 </td> </tr>
  <tr> <td align="right"> 222 </td> <td align="right"> 1825 </td> <td align="right"> 67.77 </td> </tr>
  <tr> <td align="right"> 223 </td> <td align="right"> 1830 </td> <td align="right"> 77.70 </td> </tr>
  <tr> <td align="right"> 224 </td> <td align="right"> 1835 </td> <td align="right"> 74.25 </td> </tr>
  <tr> <td align="right"> 225 </td> <td align="right"> 1840 </td> <td align="right"> 85.34 </td> </tr>
  <tr> <td align="right"> 226 </td> <td align="right"> 1845 </td> <td align="right"> 99.45 </td> </tr>
  <tr> <td align="right"> 227 </td> <td align="right"> 1850 </td> <td align="right"> 86.58 </td> </tr>
  <tr> <td align="right"> 228 </td> <td align="right"> 1855 </td> <td align="right"> 85.60 </td> </tr>
  <tr> <td align="right"> 229 </td> <td align="right"> 1900 </td> <td align="right"> 84.87 </td> </tr>
  <tr> <td align="right"> 230 </td> <td align="right"> 1905 </td> <td align="right"> 77.83 </td> </tr>
  <tr> <td align="right"> 231 </td> <td align="right"> 1910 </td> <td align="right"> 58.04 </td> </tr>
  <tr> <td align="right"> 232 </td> <td align="right"> 1915 </td> <td align="right"> 53.36 </td> </tr>
  <tr> <td align="right"> 233 </td> <td align="right"> 1920 </td> <td align="right"> 36.32 </td> </tr>
  <tr> <td align="right"> 234 </td> <td align="right"> 1925 </td> <td align="right"> 20.72 </td> </tr>
  <tr> <td align="right"> 235 </td> <td align="right"> 1930 </td> <td align="right"> 27.40 </td> </tr>
  <tr> <td align="right"> 236 </td> <td align="right"> 1935 </td> <td align="right"> 40.02 </td> </tr>
  <tr> <td align="right"> 237 </td> <td align="right"> 1940 </td> <td align="right"> 30.21 </td> </tr>
  <tr> <td align="right"> 238 </td> <td align="right"> 1945 </td> <td align="right"> 25.55 </td> </tr>
  <tr> <td align="right"> 239 </td> <td align="right"> 1950 </td> <td align="right"> 45.66 </td> </tr>
  <tr> <td align="right"> 240 </td> <td align="right"> 1955 </td> <td align="right"> 33.53 </td> </tr>
  <tr> <td align="right"> 241 </td> <td align="right"> 2000 </td> <td align="right"> 19.62 </td> </tr>
  <tr> <td align="right"> 242 </td> <td align="right"> 2005 </td> <td align="right"> 19.02 </td> </tr>
  <tr> <td align="right"> 243 </td> <td align="right"> 2010 </td> <td align="right"> 19.34 </td> </tr>
  <tr> <td align="right"> 244 </td> <td align="right"> 2015 </td> <td align="right"> 33.34 </td> </tr>
  <tr> <td align="right"> 245 </td> <td align="right"> 2020 </td> <td align="right"> 26.81 </td> </tr>
  <tr> <td align="right"> 246 </td> <td align="right"> 2025 </td> <td align="right"> 21.17 </td> </tr>
  <tr> <td align="right"> 247 </td> <td align="right"> 2030 </td> <td align="right"> 27.30 </td> </tr>
  <tr> <td align="right"> 248 </td> <td align="right"> 2035 </td> <td align="right"> 21.34 </td> </tr>
  <tr> <td align="right"> 249 </td> <td align="right"> 2040 </td> <td align="right"> 19.55 </td> </tr>
  <tr> <td align="right"> 250 </td> <td align="right"> 2045 </td> <td align="right"> 21.32 </td> </tr>
  <tr> <td align="right"> 251 </td> <td align="right"> 2050 </td> <td align="right"> 32.30 </td> </tr>
  <tr> <td align="right"> 252 </td> <td align="right"> 2055 </td> <td align="right"> 20.15 </td> </tr>
  <tr> <td align="right"> 253 </td> <td align="right"> 2100 </td> <td align="right"> 15.94 </td> </tr>
  <tr> <td align="right"> 254 </td> <td align="right"> 2105 </td> <td align="right"> 17.23 </td> </tr>
  <tr> <td align="right"> 255 </td> <td align="right"> 2110 </td> <td align="right"> 23.45 </td> </tr>
  <tr> <td align="right"> 256 </td> <td align="right"> 2115 </td> <td align="right"> 19.25 </td> </tr>
  <tr> <td align="right"> 257 </td> <td align="right"> 2120 </td> <td align="right"> 12.45 </td> </tr>
  <tr> <td align="right"> 258 </td> <td align="right"> 2125 </td> <td align="right"> 8.02 </td> </tr>
  <tr> <td align="right"> 259 </td> <td align="right"> 2130 </td> <td align="right"> 14.66 </td> </tr>
  <tr> <td align="right"> 260 </td> <td align="right"> 2135 </td> <td align="right"> 16.30 </td> </tr>
  <tr> <td align="right"> 261 </td> <td align="right"> 2140 </td> <td align="right"> 8.68 </td> </tr>
  <tr> <td align="right"> 262 </td> <td align="right"> 2145 </td> <td align="right"> 7.79 </td> </tr>
  <tr> <td align="right"> 263 </td> <td align="right"> 2150 </td> <td align="right"> 8.13 </td> </tr>
  <tr> <td align="right"> 264 </td> <td align="right"> 2155 </td> <td align="right"> 2.62 </td> </tr>
  <tr> <td align="right"> 265 </td> <td align="right"> 2200 </td> <td align="right"> 1.45 </td> </tr>
  <tr> <td align="right"> 266 </td> <td align="right"> 2205 </td> <td align="right"> 3.68 </td> </tr>
  <tr> <td align="right"> 267 </td> <td align="right"> 2210 </td> <td align="right"> 4.81 </td> </tr>
  <tr> <td align="right"> 268 </td> <td align="right"> 2215 </td> <td align="right"> 8.51 </td> </tr>
  <tr> <td align="right"> 269 </td> <td align="right"> 2220 </td> <td align="right"> 7.08 </td> </tr>
  <tr> <td align="right"> 270 </td> <td align="right"> 2225 </td> <td align="right"> 8.70 </td> </tr>
  <tr> <td align="right"> 271 </td> <td align="right"> 2230 </td> <td align="right"> 9.75 </td> </tr>
  <tr> <td align="right"> 272 </td> <td align="right"> 2235 </td> <td align="right"> 2.21 </td> </tr>
  <tr> <td align="right"> 273 </td> <td align="right"> 2240 </td> <td align="right"> 0.32 </td> </tr>
  <tr> <td align="right"> 274 </td> <td align="right"> 2245 </td> <td align="right"> 0.11 </td> </tr>
  <tr> <td align="right"> 275 </td> <td align="right"> 2250 </td> <td align="right"> 1.60 </td> </tr>
  <tr> <td align="right"> 276 </td> <td align="right"> 2255 </td> <td align="right"> 4.60 </td> </tr>
  <tr> <td align="right"> 277 </td> <td align="right"> 2300 </td> <td align="right"> 3.30 </td> </tr>
  <tr> <td align="right"> 278 </td> <td align="right"> 2305 </td> <td align="right"> 2.85 </td> </tr>
  <tr> <td align="right"> 279 </td> <td align="right"> 2310 </td> <td align="right"> 0.00 </td> </tr>
  <tr> <td align="right"> 280 </td> <td align="right"> 2315 </td> <td align="right"> 0.83 </td> </tr>
  <tr> <td align="right"> 281 </td> <td align="right"> 2320 </td> <td align="right"> 0.96 </td> </tr>
  <tr> <td align="right"> 282 </td> <td align="right"> 2325 </td> <td align="right"> 1.58 </td> </tr>
  <tr> <td align="right"> 283 </td> <td align="right"> 2330 </td> <td align="right"> 2.60 </td> </tr>
  <tr> <td align="right"> 284 </td> <td align="right"> 2335 </td> <td align="right"> 4.70 </td> </tr>
  <tr> <td align="right"> 285 </td> <td align="right"> 2340 </td> <td align="right"> 3.30 </td> </tr>
  <tr> <td align="right"> 286 </td> <td align="right"> 2345 </td> <td align="right"> 0.64 </td> </tr>
  <tr> <td align="right"> 287 </td> <td align="right"> 2350 </td> <td align="right"> 0.23 </td> </tr>
  <tr> <td align="right"> 288 </td> <td align="right"> 2355 </td> <td align="right"> 1.08 </td> </tr>
   </table>

### 3.1.1 Changing the column names for average_steps_per_interval


```r
names(average_steps_per_interval) <- c("Interval", "Steps")

average_steps_per_interval <- xtable(average_steps_per_interval)
print(average_steps_per_interval, type = "html")
```

<!-- html table generated in R 4.2.2 by xtable 1.8-4 package -->
<!-- Sun Jan 28 20:56:39 2024 -->
<table border=1>
<tr> <th>  </th> <th> Interval </th> <th> Steps </th>  </tr>
  <tr> <td align="right"> 1 </td> <td align="right">   0 </td> <td align="right"> 1.72 </td> </tr>
  <tr> <td align="right"> 2 </td> <td align="right">   5 </td> <td align="right"> 0.34 </td> </tr>
  <tr> <td align="right"> 3 </td> <td align="right">  10 </td> <td align="right"> 0.13 </td> </tr>
  <tr> <td align="right"> 4 </td> <td align="right">  15 </td> <td align="right"> 0.15 </td> </tr>
  <tr> <td align="right"> 5 </td> <td align="right">  20 </td> <td align="right"> 0.08 </td> </tr>
  <tr> <td align="right"> 6 </td> <td align="right">  25 </td> <td align="right"> 2.09 </td> </tr>
  <tr> <td align="right"> 7 </td> <td align="right">  30 </td> <td align="right"> 0.53 </td> </tr>
  <tr> <td align="right"> 8 </td> <td align="right">  35 </td> <td align="right"> 0.87 </td> </tr>
  <tr> <td align="right"> 9 </td> <td align="right">  40 </td> <td align="right"> 0.00 </td> </tr>
  <tr> <td align="right"> 10 </td> <td align="right">  45 </td> <td align="right"> 1.47 </td> </tr>
  <tr> <td align="right"> 11 </td> <td align="right">  50 </td> <td align="right"> 0.30 </td> </tr>
  <tr> <td align="right"> 12 </td> <td align="right">  55 </td> <td align="right"> 0.13 </td> </tr>
  <tr> <td align="right"> 13 </td> <td align="right"> 100 </td> <td align="right"> 0.32 </td> </tr>
  <tr> <td align="right"> 14 </td> <td align="right"> 105 </td> <td align="right"> 0.68 </td> </tr>
  <tr> <td align="right"> 15 </td> <td align="right"> 110 </td> <td align="right"> 0.15 </td> </tr>
  <tr> <td align="right"> 16 </td> <td align="right"> 115 </td> <td align="right"> 0.34 </td> </tr>
  <tr> <td align="right"> 17 </td> <td align="right"> 120 </td> <td align="right"> 0.00 </td> </tr>
  <tr> <td align="right"> 18 </td> <td align="right"> 125 </td> <td align="right"> 1.11 </td> </tr>
  <tr> <td align="right"> 19 </td> <td align="right"> 130 </td> <td align="right"> 1.83 </td> </tr>
  <tr> <td align="right"> 20 </td> <td align="right"> 135 </td> <td align="right"> 0.17 </td> </tr>
  <tr> <td align="right"> 21 </td> <td align="right"> 140 </td> <td align="right"> 0.17 </td> </tr>
  <tr> <td align="right"> 22 </td> <td align="right"> 145 </td> <td align="right"> 0.38 </td> </tr>
  <tr> <td align="right"> 23 </td> <td align="right"> 150 </td> <td align="right"> 0.26 </td> </tr>
  <tr> <td align="right"> 24 </td> <td align="right"> 155 </td> <td align="right"> 0.00 </td> </tr>
  <tr> <td align="right"> 25 </td> <td align="right"> 200 </td> <td align="right"> 0.00 </td> </tr>
  <tr> <td align="right"> 26 </td> <td align="right"> 205 </td> <td align="right"> 0.00 </td> </tr>
  <tr> <td align="right"> 27 </td> <td align="right"> 210 </td> <td align="right"> 1.13 </td> </tr>
  <tr> <td align="right"> 28 </td> <td align="right"> 215 </td> <td align="right"> 0.00 </td> </tr>
  <tr> <td align="right"> 29 </td> <td align="right"> 220 </td> <td align="right"> 0.00 </td> </tr>
  <tr> <td align="right"> 30 </td> <td align="right"> 225 </td> <td align="right"> 0.13 </td> </tr>
  <tr> <td align="right"> 31 </td> <td align="right"> 230 </td> <td align="right"> 0.00 </td> </tr>
  <tr> <td align="right"> 32 </td> <td align="right"> 235 </td> <td align="right"> 0.23 </td> </tr>
  <tr> <td align="right"> 33 </td> <td align="right"> 240 </td> <td align="right"> 0.00 </td> </tr>
  <tr> <td align="right"> 34 </td> <td align="right"> 245 </td> <td align="right"> 0.00 </td> </tr>
  <tr> <td align="right"> 35 </td> <td align="right"> 250 </td> <td align="right"> 1.55 </td> </tr>
  <tr> <td align="right"> 36 </td> <td align="right"> 255 </td> <td align="right"> 0.94 </td> </tr>
  <tr> <td align="right"> 37 </td> <td align="right"> 300 </td> <td align="right"> 0.00 </td> </tr>
  <tr> <td align="right"> 38 </td> <td align="right"> 305 </td> <td align="right"> 0.00 </td> </tr>
  <tr> <td align="right"> 39 </td> <td align="right"> 310 </td> <td align="right"> 0.00 </td> </tr>
  <tr> <td align="right"> 40 </td> <td align="right"> 315 </td> <td align="right"> 0.00 </td> </tr>
  <tr> <td align="right"> 41 </td> <td align="right"> 320 </td> <td align="right"> 0.21 </td> </tr>
  <tr> <td align="right"> 42 </td> <td align="right"> 325 </td> <td align="right"> 0.62 </td> </tr>
  <tr> <td align="right"> 43 </td> <td align="right"> 330 </td> <td align="right"> 1.62 </td> </tr>
  <tr> <td align="right"> 44 </td> <td align="right"> 335 </td> <td align="right"> 0.58 </td> </tr>
  <tr> <td align="right"> 45 </td> <td align="right"> 340 </td> <td align="right"> 0.49 </td> </tr>
  <tr> <td align="right"> 46 </td> <td align="right"> 345 </td> <td align="right"> 0.08 </td> </tr>
  <tr> <td align="right"> 47 </td> <td align="right"> 350 </td> <td align="right"> 0.00 </td> </tr>
  <tr> <td align="right"> 48 </td> <td align="right"> 355 </td> <td align="right"> 0.00 </td> </tr>
  <tr> <td align="right"> 49 </td> <td align="right"> 400 </td> <td align="right"> 1.19 </td> </tr>
  <tr> <td align="right"> 50 </td> <td align="right"> 405 </td> <td align="right"> 0.94 </td> </tr>
  <tr> <td align="right"> 51 </td> <td align="right"> 410 </td> <td align="right"> 2.57 </td> </tr>
  <tr> <td align="right"> 52 </td> <td align="right"> 415 </td> <td align="right"> 0.00 </td> </tr>
  <tr> <td align="right"> 53 </td> <td align="right"> 420 </td> <td align="right"> 0.34 </td> </tr>
  <tr> <td align="right"> 54 </td> <td align="right"> 425 </td> <td align="right"> 0.36 </td> </tr>
  <tr> <td align="right"> 55 </td> <td align="right"> 430 </td> <td align="right"> 4.11 </td> </tr>
  <tr> <td align="right"> 56 </td> <td align="right"> 435 </td> <td align="right"> 0.66 </td> </tr>
  <tr> <td align="right"> 57 </td> <td align="right"> 440 </td> <td align="right"> 3.49 </td> </tr>
  <tr> <td align="right"> 58 </td> <td align="right"> 445 </td> <td align="right"> 0.83 </td> </tr>
  <tr> <td align="right"> 59 </td> <td align="right"> 450 </td> <td align="right"> 3.11 </td> </tr>
  <tr> <td align="right"> 60 </td> <td align="right"> 455 </td> <td align="right"> 1.11 </td> </tr>
  <tr> <td align="right"> 61 </td> <td align="right"> 500 </td> <td align="right"> 0.00 </td> </tr>
  <tr> <td align="right"> 62 </td> <td align="right"> 505 </td> <td align="right"> 1.57 </td> </tr>
  <tr> <td align="right"> 63 </td> <td align="right"> 510 </td> <td align="right"> 3.00 </td> </tr>
  <tr> <td align="right"> 64 </td> <td align="right"> 515 </td> <td align="right"> 2.25 </td> </tr>
  <tr> <td align="right"> 65 </td> <td align="right"> 520 </td> <td align="right"> 3.32 </td> </tr>
  <tr> <td align="right"> 66 </td> <td align="right"> 525 </td> <td align="right"> 2.96 </td> </tr>
  <tr> <td align="right"> 67 </td> <td align="right"> 530 </td> <td align="right"> 2.09 </td> </tr>
  <tr> <td align="right"> 68 </td> <td align="right"> 535 </td> <td align="right"> 6.06 </td> </tr>
  <tr> <td align="right"> 69 </td> <td align="right"> 540 </td> <td align="right"> 16.02 </td> </tr>
  <tr> <td align="right"> 70 </td> <td align="right"> 545 </td> <td align="right"> 18.34 </td> </tr>
  <tr> <td align="right"> 71 </td> <td align="right"> 550 </td> <td align="right"> 39.45 </td> </tr>
  <tr> <td align="right"> 72 </td> <td align="right"> 555 </td> <td align="right"> 44.49 </td> </tr>
  <tr> <td align="right"> 73 </td> <td align="right"> 600 </td> <td align="right"> 31.49 </td> </tr>
  <tr> <td align="right"> 74 </td> <td align="right"> 605 </td> <td align="right"> 49.26 </td> </tr>
  <tr> <td align="right"> 75 </td> <td align="right"> 610 </td> <td align="right"> 53.77 </td> </tr>
  <tr> <td align="right"> 76 </td> <td align="right"> 615 </td> <td align="right"> 63.45 </td> </tr>
  <tr> <td align="right"> 77 </td> <td align="right"> 620 </td> <td align="right"> 49.96 </td> </tr>
  <tr> <td align="right"> 78 </td> <td align="right"> 625 </td> <td align="right"> 47.08 </td> </tr>
  <tr> <td align="right"> 79 </td> <td align="right"> 630 </td> <td align="right"> 52.15 </td> </tr>
  <tr> <td align="right"> 80 </td> <td align="right"> 635 </td> <td align="right"> 39.34 </td> </tr>
  <tr> <td align="right"> 81 </td> <td align="right"> 640 </td> <td align="right"> 44.02 </td> </tr>
  <tr> <td align="right"> 82 </td> <td align="right"> 645 </td> <td align="right"> 44.17 </td> </tr>
  <tr> <td align="right"> 83 </td> <td align="right"> 650 </td> <td align="right"> 37.36 </td> </tr>
  <tr> <td align="right"> 84 </td> <td align="right"> 655 </td> <td align="right"> 49.04 </td> </tr>
  <tr> <td align="right"> 85 </td> <td align="right"> 700 </td> <td align="right"> 43.81 </td> </tr>
  <tr> <td align="right"> 86 </td> <td align="right"> 705 </td> <td align="right"> 44.38 </td> </tr>
  <tr> <td align="right"> 87 </td> <td align="right"> 710 </td> <td align="right"> 50.51 </td> </tr>
  <tr> <td align="right"> 88 </td> <td align="right"> 715 </td> <td align="right"> 54.51 </td> </tr>
  <tr> <td align="right"> 89 </td> <td align="right"> 720 </td> <td align="right"> 49.92 </td> </tr>
  <tr> <td align="right"> 90 </td> <td align="right"> 725 </td> <td align="right"> 50.98 </td> </tr>
  <tr> <td align="right"> 91 </td> <td align="right"> 730 </td> <td align="right"> 55.68 </td> </tr>
  <tr> <td align="right"> 92 </td> <td align="right"> 735 </td> <td align="right"> 44.32 </td> </tr>
  <tr> <td align="right"> 93 </td> <td align="right"> 740 </td> <td align="right"> 52.26 </td> </tr>
  <tr> <td align="right"> 94 </td> <td align="right"> 745 </td> <td align="right"> 69.55 </td> </tr>
  <tr> <td align="right"> 95 </td> <td align="right"> 750 </td> <td align="right"> 57.85 </td> </tr>
  <tr> <td align="right"> 96 </td> <td align="right"> 755 </td> <td align="right"> 56.15 </td> </tr>
  <tr> <td align="right"> 97 </td> <td align="right"> 800 </td> <td align="right"> 73.38 </td> </tr>
  <tr> <td align="right"> 98 </td> <td align="right"> 805 </td> <td align="right"> 68.21 </td> </tr>
  <tr> <td align="right"> 99 </td> <td align="right"> 810 </td> <td align="right"> 129.43 </td> </tr>
  <tr> <td align="right"> 100 </td> <td align="right"> 815 </td> <td align="right"> 157.53 </td> </tr>
  <tr> <td align="right"> 101 </td> <td align="right"> 820 </td> <td align="right"> 171.15 </td> </tr>
  <tr> <td align="right"> 102 </td> <td align="right"> 825 </td> <td align="right"> 155.40 </td> </tr>
  <tr> <td align="right"> 103 </td> <td align="right"> 830 </td> <td align="right"> 177.30 </td> </tr>
  <tr> <td align="right"> 104 </td> <td align="right"> 835 </td> <td align="right"> 206.17 </td> </tr>
  <tr> <td align="right"> 105 </td> <td align="right"> 840 </td> <td align="right"> 195.92 </td> </tr>
  <tr> <td align="right"> 106 </td> <td align="right"> 845 </td> <td align="right"> 179.57 </td> </tr>
  <tr> <td align="right"> 107 </td> <td align="right"> 850 </td> <td align="right"> 183.40 </td> </tr>
  <tr> <td align="right"> 108 </td> <td align="right"> 855 </td> <td align="right"> 167.02 </td> </tr>
  <tr> <td align="right"> 109 </td> <td align="right"> 900 </td> <td align="right"> 143.45 </td> </tr>
  <tr> <td align="right"> 110 </td> <td align="right"> 905 </td> <td align="right"> 124.04 </td> </tr>
  <tr> <td align="right"> 111 </td> <td align="right"> 910 </td> <td align="right"> 109.11 </td> </tr>
  <tr> <td align="right"> 112 </td> <td align="right"> 915 </td> <td align="right"> 108.11 </td> </tr>
  <tr> <td align="right"> 113 </td> <td align="right"> 920 </td> <td align="right"> 103.72 </td> </tr>
  <tr> <td align="right"> 114 </td> <td align="right"> 925 </td> <td align="right"> 95.96 </td> </tr>
  <tr> <td align="right"> 115 </td> <td align="right"> 930 </td> <td align="right"> 66.21 </td> </tr>
  <tr> <td align="right"> 116 </td> <td align="right"> 935 </td> <td align="right"> 45.23 </td> </tr>
  <tr> <td align="right"> 117 </td> <td align="right"> 940 </td> <td align="right"> 24.79 </td> </tr>
  <tr> <td align="right"> 118 </td> <td align="right"> 945 </td> <td align="right"> 38.75 </td> </tr>
  <tr> <td align="right"> 119 </td> <td align="right"> 950 </td> <td align="right"> 34.98 </td> </tr>
  <tr> <td align="right"> 120 </td> <td align="right"> 955 </td> <td align="right"> 21.06 </td> </tr>
  <tr> <td align="right"> 121 </td> <td align="right"> 1000 </td> <td align="right"> 40.57 </td> </tr>
  <tr> <td align="right"> 122 </td> <td align="right"> 1005 </td> <td align="right"> 26.98 </td> </tr>
  <tr> <td align="right"> 123 </td> <td align="right"> 1010 </td> <td align="right"> 42.42 </td> </tr>
  <tr> <td align="right"> 124 </td> <td align="right"> 1015 </td> <td align="right"> 52.66 </td> </tr>
  <tr> <td align="right"> 125 </td> <td align="right"> 1020 </td> <td align="right"> 38.92 </td> </tr>
  <tr> <td align="right"> 126 </td> <td align="right"> 1025 </td> <td align="right"> 50.79 </td> </tr>
  <tr> <td align="right"> 127 </td> <td align="right"> 1030 </td> <td align="right"> 44.28 </td> </tr>
  <tr> <td align="right"> 128 </td> <td align="right"> 1035 </td> <td align="right"> 37.42 </td> </tr>
  <tr> <td align="right"> 129 </td> <td align="right"> 1040 </td> <td align="right"> 34.70 </td> </tr>
  <tr> <td align="right"> 130 </td> <td align="right"> 1045 </td> <td align="right"> 28.34 </td> </tr>
  <tr> <td align="right"> 131 </td> <td align="right"> 1050 </td> <td align="right"> 25.09 </td> </tr>
  <tr> <td align="right"> 132 </td> <td align="right"> 1055 </td> <td align="right"> 31.94 </td> </tr>
  <tr> <td align="right"> 133 </td> <td align="right"> 1100 </td> <td align="right"> 31.36 </td> </tr>
  <tr> <td align="right"> 134 </td> <td align="right"> 1105 </td> <td align="right"> 29.68 </td> </tr>
  <tr> <td align="right"> 135 </td> <td align="right"> 1110 </td> <td align="right"> 21.32 </td> </tr>
  <tr> <td align="right"> 136 </td> <td align="right"> 1115 </td> <td align="right"> 25.55 </td> </tr>
  <tr> <td align="right"> 137 </td> <td align="right"> 1120 </td> <td align="right"> 28.38 </td> </tr>
  <tr> <td align="right"> 138 </td> <td align="right"> 1125 </td> <td align="right"> 26.47 </td> </tr>
  <tr> <td align="right"> 139 </td> <td align="right"> 1130 </td> <td align="right"> 33.43 </td> </tr>
  <tr> <td align="right"> 140 </td> <td align="right"> 1135 </td> <td align="right"> 49.98 </td> </tr>
  <tr> <td align="right"> 141 </td> <td align="right"> 1140 </td> <td align="right"> 42.04 </td> </tr>
  <tr> <td align="right"> 142 </td> <td align="right"> 1145 </td> <td align="right"> 44.60 </td> </tr>
  <tr> <td align="right"> 143 </td> <td align="right"> 1150 </td> <td align="right"> 46.04 </td> </tr>
  <tr> <td align="right"> 144 </td> <td align="right"> 1155 </td> <td align="right"> 59.19 </td> </tr>
  <tr> <td align="right"> 145 </td> <td align="right"> 1200 </td> <td align="right"> 63.87 </td> </tr>
  <tr> <td align="right"> 146 </td> <td align="right"> 1205 </td> <td align="right"> 87.70 </td> </tr>
  <tr> <td align="right"> 147 </td> <td align="right"> 1210 </td> <td align="right"> 94.85 </td> </tr>
  <tr> <td align="right"> 148 </td> <td align="right"> 1215 </td> <td align="right"> 92.77 </td> </tr>
  <tr> <td align="right"> 149 </td> <td align="right"> 1220 </td> <td align="right"> 63.40 </td> </tr>
  <tr> <td align="right"> 150 </td> <td align="right"> 1225 </td> <td align="right"> 50.17 </td> </tr>
  <tr> <td align="right"> 151 </td> <td align="right"> 1230 </td> <td align="right"> 54.47 </td> </tr>
  <tr> <td align="right"> 152 </td> <td align="right"> 1235 </td> <td align="right"> 32.42 </td> </tr>
  <tr> <td align="right"> 153 </td> <td align="right"> 1240 </td> <td align="right"> 26.53 </td> </tr>
  <tr> <td align="right"> 154 </td> <td align="right"> 1245 </td> <td align="right"> 37.74 </td> </tr>
  <tr> <td align="right"> 155 </td> <td align="right"> 1250 </td> <td align="right"> 45.06 </td> </tr>
  <tr> <td align="right"> 156 </td> <td align="right"> 1255 </td> <td align="right"> 67.28 </td> </tr>
  <tr> <td align="right"> 157 </td> <td align="right"> 1300 </td> <td align="right"> 42.34 </td> </tr>
  <tr> <td align="right"> 158 </td> <td align="right"> 1305 </td> <td align="right"> 39.89 </td> </tr>
  <tr> <td align="right"> 159 </td> <td align="right"> 1310 </td> <td align="right"> 43.26 </td> </tr>
  <tr> <td align="right"> 160 </td> <td align="right"> 1315 </td> <td align="right"> 40.98 </td> </tr>
  <tr> <td align="right"> 161 </td> <td align="right"> 1320 </td> <td align="right"> 46.25 </td> </tr>
  <tr> <td align="right"> 162 </td> <td align="right"> 1325 </td> <td align="right"> 56.43 </td> </tr>
  <tr> <td align="right"> 163 </td> <td align="right"> 1330 </td> <td align="right"> 42.75 </td> </tr>
  <tr> <td align="right"> 164 </td> <td align="right"> 1335 </td> <td align="right"> 25.13 </td> </tr>
  <tr> <td align="right"> 165 </td> <td align="right"> 1340 </td> <td align="right"> 39.96 </td> </tr>
  <tr> <td align="right"> 166 </td> <td align="right"> 1345 </td> <td align="right"> 53.55 </td> </tr>
  <tr> <td align="right"> 167 </td> <td align="right"> 1350 </td> <td align="right"> 47.32 </td> </tr>
  <tr> <td align="right"> 168 </td> <td align="right"> 1355 </td> <td align="right"> 60.81 </td> </tr>
  <tr> <td align="right"> 169 </td> <td align="right"> 1400 </td> <td align="right"> 55.75 </td> </tr>
  <tr> <td align="right"> 170 </td> <td align="right"> 1405 </td> <td align="right"> 51.96 </td> </tr>
  <tr> <td align="right"> 171 </td> <td align="right"> 1410 </td> <td align="right"> 43.58 </td> </tr>
  <tr> <td align="right"> 172 </td> <td align="right"> 1415 </td> <td align="right"> 48.70 </td> </tr>
  <tr> <td align="right"> 173 </td> <td align="right"> 1420 </td> <td align="right"> 35.47 </td> </tr>
  <tr> <td align="right"> 174 </td> <td align="right"> 1425 </td> <td align="right"> 37.55 </td> </tr>
  <tr> <td align="right"> 175 </td> <td align="right"> 1430 </td> <td align="right"> 41.85 </td> </tr>
  <tr> <td align="right"> 176 </td> <td align="right"> 1435 </td> <td align="right"> 27.51 </td> </tr>
  <tr> <td align="right"> 177 </td> <td align="right"> 1440 </td> <td align="right"> 17.11 </td> </tr>
  <tr> <td align="right"> 178 </td> <td align="right"> 1445 </td> <td align="right"> 26.08 </td> </tr>
  <tr> <td align="right"> 179 </td> <td align="right"> 1450 </td> <td align="right"> 43.62 </td> </tr>
  <tr> <td align="right"> 180 </td> <td align="right"> 1455 </td> <td align="right"> 43.77 </td> </tr>
  <tr> <td align="right"> 181 </td> <td align="right"> 1500 </td> <td align="right"> 30.02 </td> </tr>
  <tr> <td align="right"> 182 </td> <td align="right"> 1505 </td> <td align="right"> 36.08 </td> </tr>
  <tr> <td align="right"> 183 </td> <td align="right"> 1510 </td> <td align="right"> 35.49 </td> </tr>
  <tr> <td align="right"> 184 </td> <td align="right"> 1515 </td> <td align="right"> 38.85 </td> </tr>
  <tr> <td align="right"> 185 </td> <td align="right"> 1520 </td> <td align="right"> 45.96 </td> </tr>
  <tr> <td align="right"> 186 </td> <td align="right"> 1525 </td> <td align="right"> 47.75 </td> </tr>
  <tr> <td align="right"> 187 </td> <td align="right"> 1530 </td> <td align="right"> 48.13 </td> </tr>
  <tr> <td align="right"> 188 </td> <td align="right"> 1535 </td> <td align="right"> 65.32 </td> </tr>
  <tr> <td align="right"> 189 </td> <td align="right"> 1540 </td> <td align="right"> 82.91 </td> </tr>
  <tr> <td align="right"> 190 </td> <td align="right"> 1545 </td> <td align="right"> 98.66 </td> </tr>
  <tr> <td align="right"> 191 </td> <td align="right"> 1550 </td> <td align="right"> 102.11 </td> </tr>
  <tr> <td align="right"> 192 </td> <td align="right"> 1555 </td> <td align="right"> 83.96 </td> </tr>
  <tr> <td align="right"> 193 </td> <td align="right"> 1600 </td> <td align="right"> 62.13 </td> </tr>
  <tr> <td align="right"> 194 </td> <td align="right"> 1605 </td> <td align="right"> 64.13 </td> </tr>
  <tr> <td align="right"> 195 </td> <td align="right"> 1610 </td> <td align="right"> 74.55 </td> </tr>
  <tr> <td align="right"> 196 </td> <td align="right"> 1615 </td> <td align="right"> 63.17 </td> </tr>
  <tr> <td align="right"> 197 </td> <td align="right"> 1620 </td> <td align="right"> 56.91 </td> </tr>
  <tr> <td align="right"> 198 </td> <td align="right"> 1625 </td> <td align="right"> 59.77 </td> </tr>
  <tr> <td align="right"> 199 </td> <td align="right"> 1630 </td> <td align="right"> 43.87 </td> </tr>
  <tr> <td align="right"> 200 </td> <td align="right"> 1635 </td> <td align="right"> 38.57 </td> </tr>
  <tr> <td align="right"> 201 </td> <td align="right"> 1640 </td> <td align="right"> 44.66 </td> </tr>
  <tr> <td align="right"> 202 </td> <td align="right"> 1645 </td> <td align="right"> 45.45 </td> </tr>
  <tr> <td align="right"> 203 </td> <td align="right"> 1650 </td> <td align="right"> 46.21 </td> </tr>
  <tr> <td align="right"> 204 </td> <td align="right"> 1655 </td> <td align="right"> 43.68 </td> </tr>
  <tr> <td align="right"> 205 </td> <td align="right"> 1700 </td> <td align="right"> 46.62 </td> </tr>
  <tr> <td align="right"> 206 </td> <td align="right"> 1705 </td> <td align="right"> 56.30 </td> </tr>
  <tr> <td align="right"> 207 </td> <td align="right"> 1710 </td> <td align="right"> 50.72 </td> </tr>
  <tr> <td align="right"> 208 </td> <td align="right"> 1715 </td> <td align="right"> 61.23 </td> </tr>
  <tr> <td align="right"> 209 </td> <td align="right"> 1720 </td> <td align="right"> 72.72 </td> </tr>
  <tr> <td align="right"> 210 </td> <td align="right"> 1725 </td> <td align="right"> 78.94 </td> </tr>
  <tr> <td align="right"> 211 </td> <td align="right"> 1730 </td> <td align="right"> 68.94 </td> </tr>
  <tr> <td align="right"> 212 </td> <td align="right"> 1735 </td> <td align="right"> 59.66 </td> </tr>
  <tr> <td align="right"> 213 </td> <td align="right"> 1740 </td> <td align="right"> 75.09 </td> </tr>
  <tr> <td align="right"> 214 </td> <td align="right"> 1745 </td> <td align="right"> 56.51 </td> </tr>
  <tr> <td align="right"> 215 </td> <td align="right"> 1750 </td> <td align="right"> 34.77 </td> </tr>
  <tr> <td align="right"> 216 </td> <td align="right"> 1755 </td> <td align="right"> 37.45 </td> </tr>
  <tr> <td align="right"> 217 </td> <td align="right"> 1800 </td> <td align="right"> 40.68 </td> </tr>
  <tr> <td align="right"> 218 </td> <td align="right"> 1805 </td> <td align="right"> 58.02 </td> </tr>
  <tr> <td align="right"> 219 </td> <td align="right"> 1810 </td> <td align="right"> 74.70 </td> </tr>
  <tr> <td align="right"> 220 </td> <td align="right"> 1815 </td> <td align="right"> 85.32 </td> </tr>
  <tr> <td align="right"> 221 </td> <td align="right"> 1820 </td> <td align="right"> 59.26 </td> </tr>
  <tr> <td align="right"> 222 </td> <td align="right"> 1825 </td> <td align="right"> 67.77 </td> </tr>
  <tr> <td align="right"> 223 </td> <td align="right"> 1830 </td> <td align="right"> 77.70 </td> </tr>
  <tr> <td align="right"> 224 </td> <td align="right"> 1835 </td> <td align="right"> 74.25 </td> </tr>
  <tr> <td align="right"> 225 </td> <td align="right"> 1840 </td> <td align="right"> 85.34 </td> </tr>
  <tr> <td align="right"> 226 </td> <td align="right"> 1845 </td> <td align="right"> 99.45 </td> </tr>
  <tr> <td align="right"> 227 </td> <td align="right"> 1850 </td> <td align="right"> 86.58 </td> </tr>
  <tr> <td align="right"> 228 </td> <td align="right"> 1855 </td> <td align="right"> 85.60 </td> </tr>
  <tr> <td align="right"> 229 </td> <td align="right"> 1900 </td> <td align="right"> 84.87 </td> </tr>
  <tr> <td align="right"> 230 </td> <td align="right"> 1905 </td> <td align="right"> 77.83 </td> </tr>
  <tr> <td align="right"> 231 </td> <td align="right"> 1910 </td> <td align="right"> 58.04 </td> </tr>
  <tr> <td align="right"> 232 </td> <td align="right"> 1915 </td> <td align="right"> 53.36 </td> </tr>
  <tr> <td align="right"> 233 </td> <td align="right"> 1920 </td> <td align="right"> 36.32 </td> </tr>
  <tr> <td align="right"> 234 </td> <td align="right"> 1925 </td> <td align="right"> 20.72 </td> </tr>
  <tr> <td align="right"> 235 </td> <td align="right"> 1930 </td> <td align="right"> 27.40 </td> </tr>
  <tr> <td align="right"> 236 </td> <td align="right"> 1935 </td> <td align="right"> 40.02 </td> </tr>
  <tr> <td align="right"> 237 </td> <td align="right"> 1940 </td> <td align="right"> 30.21 </td> </tr>
  <tr> <td align="right"> 238 </td> <td align="right"> 1945 </td> <td align="right"> 25.55 </td> </tr>
  <tr> <td align="right"> 239 </td> <td align="right"> 1950 </td> <td align="right"> 45.66 </td> </tr>
  <tr> <td align="right"> 240 </td> <td align="right"> 1955 </td> <td align="right"> 33.53 </td> </tr>
  <tr> <td align="right"> 241 </td> <td align="right"> 2000 </td> <td align="right"> 19.62 </td> </tr>
  <tr> <td align="right"> 242 </td> <td align="right"> 2005 </td> <td align="right"> 19.02 </td> </tr>
  <tr> <td align="right"> 243 </td> <td align="right"> 2010 </td> <td align="right"> 19.34 </td> </tr>
  <tr> <td align="right"> 244 </td> <td align="right"> 2015 </td> <td align="right"> 33.34 </td> </tr>
  <tr> <td align="right"> 245 </td> <td align="right"> 2020 </td> <td align="right"> 26.81 </td> </tr>
  <tr> <td align="right"> 246 </td> <td align="right"> 2025 </td> <td align="right"> 21.17 </td> </tr>
  <tr> <td align="right"> 247 </td> <td align="right"> 2030 </td> <td align="right"> 27.30 </td> </tr>
  <tr> <td align="right"> 248 </td> <td align="right"> 2035 </td> <td align="right"> 21.34 </td> </tr>
  <tr> <td align="right"> 249 </td> <td align="right"> 2040 </td> <td align="right"> 19.55 </td> </tr>
  <tr> <td align="right"> 250 </td> <td align="right"> 2045 </td> <td align="right"> 21.32 </td> </tr>
  <tr> <td align="right"> 251 </td> <td align="right"> 2050 </td> <td align="right"> 32.30 </td> </tr>
  <tr> <td align="right"> 252 </td> <td align="right"> 2055 </td> <td align="right"> 20.15 </td> </tr>
  <tr> <td align="right"> 253 </td> <td align="right"> 2100 </td> <td align="right"> 15.94 </td> </tr>
  <tr> <td align="right"> 254 </td> <td align="right"> 2105 </td> <td align="right"> 17.23 </td> </tr>
  <tr> <td align="right"> 255 </td> <td align="right"> 2110 </td> <td align="right"> 23.45 </td> </tr>
  <tr> <td align="right"> 256 </td> <td align="right"> 2115 </td> <td align="right"> 19.25 </td> </tr>
  <tr> <td align="right"> 257 </td> <td align="right"> 2120 </td> <td align="right"> 12.45 </td> </tr>
  <tr> <td align="right"> 258 </td> <td align="right"> 2125 </td> <td align="right"> 8.02 </td> </tr>
  <tr> <td align="right"> 259 </td> <td align="right"> 2130 </td> <td align="right"> 14.66 </td> </tr>
  <tr> <td align="right"> 260 </td> <td align="right"> 2135 </td> <td align="right"> 16.30 </td> </tr>
  <tr> <td align="right"> 261 </td> <td align="right"> 2140 </td> <td align="right"> 8.68 </td> </tr>
  <tr> <td align="right"> 262 </td> <td align="right"> 2145 </td> <td align="right"> 7.79 </td> </tr>
  <tr> <td align="right"> 263 </td> <td align="right"> 2150 </td> <td align="right"> 8.13 </td> </tr>
  <tr> <td align="right"> 264 </td> <td align="right"> 2155 </td> <td align="right"> 2.62 </td> </tr>
  <tr> <td align="right"> 265 </td> <td align="right"> 2200 </td> <td align="right"> 1.45 </td> </tr>
  <tr> <td align="right"> 266 </td> <td align="right"> 2205 </td> <td align="right"> 3.68 </td> </tr>
  <tr> <td align="right"> 267 </td> <td align="right"> 2210 </td> <td align="right"> 4.81 </td> </tr>
  <tr> <td align="right"> 268 </td> <td align="right"> 2215 </td> <td align="right"> 8.51 </td> </tr>
  <tr> <td align="right"> 269 </td> <td align="right"> 2220 </td> <td align="right"> 7.08 </td> </tr>
  <tr> <td align="right"> 270 </td> <td align="right"> 2225 </td> <td align="right"> 8.70 </td> </tr>
  <tr> <td align="right"> 271 </td> <td align="right"> 2230 </td> <td align="right"> 9.75 </td> </tr>
  <tr> <td align="right"> 272 </td> <td align="right"> 2235 </td> <td align="right"> 2.21 </td> </tr>
  <tr> <td align="right"> 273 </td> <td align="right"> 2240 </td> <td align="right"> 0.32 </td> </tr>
  <tr> <td align="right"> 274 </td> <td align="right"> 2245 </td> <td align="right"> 0.11 </td> </tr>
  <tr> <td align="right"> 275 </td> <td align="right"> 2250 </td> <td align="right"> 1.60 </td> </tr>
  <tr> <td align="right"> 276 </td> <td align="right"> 2255 </td> <td align="right"> 4.60 </td> </tr>
  <tr> <td align="right"> 277 </td> <td align="right"> 2300 </td> <td align="right"> 3.30 </td> </tr>
  <tr> <td align="right"> 278 </td> <td align="right"> 2305 </td> <td align="right"> 2.85 </td> </tr>
  <tr> <td align="right"> 279 </td> <td align="right"> 2310 </td> <td align="right"> 0.00 </td> </tr>
  <tr> <td align="right"> 280 </td> <td align="right"> 2315 </td> <td align="right"> 0.83 </td> </tr>
  <tr> <td align="right"> 281 </td> <td align="right"> 2320 </td> <td align="right"> 0.96 </td> </tr>
  <tr> <td align="right"> 282 </td> <td align="right"> 2325 </td> <td align="right"> 1.58 </td> </tr>
  <tr> <td align="right"> 283 </td> <td align="right"> 2330 </td> <td align="right"> 2.60 </td> </tr>
  <tr> <td align="right"> 284 </td> <td align="right"> 2335 </td> <td align="right"> 4.70 </td> </tr>
  <tr> <td align="right"> 285 </td> <td align="right"> 2340 </td> <td align="right"> 3.30 </td> </tr>
  <tr> <td align="right"> 286 </td> <td align="right"> 2345 </td> <td align="right"> 0.64 </td> </tr>
  <tr> <td align="right"> 287 </td> <td align="right"> 2350 </td> <td align="right"> 0.23 </td> </tr>
  <tr> <td align="right"> 288 </td> <td align="right"> 2355 </td> <td align="right"> 1.08 </td> </tr>
   </table>

### 3.1.2 Time series plot of the 5-minute interval and the average number of steps taken, averaged across all days.


```r
library(ggplot2)
ggplot(data = average_steps_per_interval, aes(x = Interval, y = Steps)) +
    geom_line() + 
    ggtitle("Time series plot of the average number of steps taken") + 
    xlab("Interval") + 
    ylab("Average number of steps taken")
```

![](PA1_template_files/figure-html/TimeSeriesPlot-1.png)<!-- -->

### 3.2 Which 5-minute interval, on average across all the days in the dataset, contains the maximum number of steps?

The 5-minute interval which contains the maximum number of steps, on average across all the days in the dataset is:


```r
average_steps_per_interval[which.max(average_steps_per_interval$Steps), ]$Interval
```

[1] 835

## 4. Imputing missing values

### 4.1 Calculate and report the total number of missing values in the dataset (i.e. the total number of rows with NAs)

Total number of rows with NAs:


```r
sum(is.na(activity$steps))
```

[1] 2304

### 4.2 Devise a strategy for filling in all of the missing values in the dataset. The strategy does not need to be sophisticated. For example, you could use the mean/median for that day, or the mean for that 5-minute interval, etc.

### 4.2.1 Replacing the NAs row with the average daily activity pattern (5-minute interval)


```r
mean <- mean(average_steps_per_interval$Steps)
print(mean)
```

[1] 37.3826

### 4.3 Create a new dataset that is equal to the original dataset but with the missing data filled in.

### 4.3.1 Transforming steps column in activity table with the mean if they are NAs


```r
new_activity <- transform(activity, 
                              steps = ifelse(is.na(activity$steps), 
                                             yes = mean,
                                             no = activity$steps))

head <- xtable(head(new_activity))
print(head, type = "html")
```

<!-- html table generated in R 4.2.2 by xtable 1.8-4 package -->
<!-- Sun Jan 28 20:56:40 2024 -->
<table border=1>
<tr> <th>  </th> <th> steps </th> <th> date </th> <th> interval </th>  </tr>
  <tr> <td align="right"> 1 </td> <td align="right"> 37.38 </td> <td> 2012-10-01 </td> <td align="right">   0 </td> </tr>
  <tr> <td align="right"> 2 </td> <td align="right"> 37.38 </td> <td> 2012-10-01 </td> <td align="right">   5 </td> </tr>
  <tr> <td align="right"> 3 </td> <td align="right"> 37.38 </td> <td> 2012-10-01 </td> <td align="right">  10 </td> </tr>
  <tr> <td align="right"> 4 </td> <td align="right"> 37.38 </td> <td> 2012-10-01 </td> <td align="right">  15 </td> </tr>
  <tr> <td align="right"> 5 </td> <td align="right"> 37.38 </td> <td> 2012-10-01 </td> <td align="right">  20 </td> </tr>
  <tr> <td align="right"> 6 </td> <td align="right"> 37.38 </td> <td> 2012-10-01 </td> <td align="right">  25 </td> </tr>
   </table>

### 4.4 Make a histogram of the total number of steps taken each day and Calculate and report the mean and median total number of steps taken per day. Do these values differ from the estimates from the first part of the assignment? What is the impact of imputing missing data on the estimates of the total daily number of steps?

### 4.4.1 Calculate the total number of steps taken per day after imputing the missing values


```r
new_total_steps_per_day <- aggregate(steps ~ date, new_activity, sum)

new_total_steps_per_day <- xtable(new_total_steps_per_day)
print(new_total_steps_per_day, type = "html")
```

<!-- html table generated in R 4.2.2 by xtable 1.8-4 package -->
<!-- Sun Jan 28 20:56:40 2024 -->
<table border=1>
<tr> <th>  </th> <th> date </th> <th> steps </th>  </tr>
  <tr> <td align="right"> 1 </td> <td> 2012-10-01 </td> <td align="right"> 10766.19 </td> </tr>
  <tr> <td align="right"> 2 </td> <td> 2012-10-02 </td> <td align="right"> 126.00 </td> </tr>
  <tr> <td align="right"> 3 </td> <td> 2012-10-03 </td> <td align="right"> 11352.00 </td> </tr>
  <tr> <td align="right"> 4 </td> <td> 2012-10-04 </td> <td align="right"> 12116.00 </td> </tr>
  <tr> <td align="right"> 5 </td> <td> 2012-10-05 </td> <td align="right"> 13294.00 </td> </tr>
  <tr> <td align="right"> 6 </td> <td> 2012-10-06 </td> <td align="right"> 15420.00 </td> </tr>
  <tr> <td align="right"> 7 </td> <td> 2012-10-07 </td> <td align="right"> 11015.00 </td> </tr>
  <tr> <td align="right"> 8 </td> <td> 2012-10-08 </td> <td align="right"> 10766.19 </td> </tr>
  <tr> <td align="right"> 9 </td> <td> 2012-10-09 </td> <td align="right"> 12811.00 </td> </tr>
  <tr> <td align="right"> 10 </td> <td> 2012-10-10 </td> <td align="right"> 9900.00 </td> </tr>
  <tr> <td align="right"> 11 </td> <td> 2012-10-11 </td> <td align="right"> 10304.00 </td> </tr>
  <tr> <td align="right"> 12 </td> <td> 2012-10-12 </td> <td align="right"> 17382.00 </td> </tr>
  <tr> <td align="right"> 13 </td> <td> 2012-10-13 </td> <td align="right"> 12426.00 </td> </tr>
  <tr> <td align="right"> 14 </td> <td> 2012-10-14 </td> <td align="right"> 15098.00 </td> </tr>
  <tr> <td align="right"> 15 </td> <td> 2012-10-15 </td> <td align="right"> 10139.00 </td> </tr>
  <tr> <td align="right"> 16 </td> <td> 2012-10-16 </td> <td align="right"> 15084.00 </td> </tr>
  <tr> <td align="right"> 17 </td> <td> 2012-10-17 </td> <td align="right"> 13452.00 </td> </tr>
  <tr> <td align="right"> 18 </td> <td> 2012-10-18 </td> <td align="right"> 10056.00 </td> </tr>
  <tr> <td align="right"> 19 </td> <td> 2012-10-19 </td> <td align="right"> 11829.00 </td> </tr>
  <tr> <td align="right"> 20 </td> <td> 2012-10-20 </td> <td align="right"> 10395.00 </td> </tr>
  <tr> <td align="right"> 21 </td> <td> 2012-10-21 </td> <td align="right"> 8821.00 </td> </tr>
  <tr> <td align="right"> 22 </td> <td> 2012-10-22 </td> <td align="right"> 13460.00 </td> </tr>
  <tr> <td align="right"> 23 </td> <td> 2012-10-23 </td> <td align="right"> 8918.00 </td> </tr>
  <tr> <td align="right"> 24 </td> <td> 2012-10-24 </td> <td align="right"> 8355.00 </td> </tr>
  <tr> <td align="right"> 25 </td> <td> 2012-10-25 </td> <td align="right"> 2492.00 </td> </tr>
  <tr> <td align="right"> 26 </td> <td> 2012-10-26 </td> <td align="right"> 6778.00 </td> </tr>
  <tr> <td align="right"> 27 </td> <td> 2012-10-27 </td> <td align="right"> 10119.00 </td> </tr>
  <tr> <td align="right"> 28 </td> <td> 2012-10-28 </td> <td align="right"> 11458.00 </td> </tr>
  <tr> <td align="right"> 29 </td> <td> 2012-10-29 </td> <td align="right"> 5018.00 </td> </tr>
  <tr> <td align="right"> 30 </td> <td> 2012-10-30 </td> <td align="right"> 9819.00 </td> </tr>
  <tr> <td align="right"> 31 </td> <td> 2012-10-31 </td> <td align="right"> 15414.00 </td> </tr>
  <tr> <td align="right"> 32 </td> <td> 2012-11-01 </td> <td align="right"> 10766.19 </td> </tr>
  <tr> <td align="right"> 33 </td> <td> 2012-11-02 </td> <td align="right"> 10600.00 </td> </tr>
  <tr> <td align="right"> 34 </td> <td> 2012-11-03 </td> <td align="right"> 10571.00 </td> </tr>
  <tr> <td align="right"> 35 </td> <td> 2012-11-04 </td> <td align="right"> 10766.19 </td> </tr>
  <tr> <td align="right"> 36 </td> <td> 2012-11-05 </td> <td align="right"> 10439.00 </td> </tr>
  <tr> <td align="right"> 37 </td> <td> 2012-11-06 </td> <td align="right"> 8334.00 </td> </tr>
  <tr> <td align="right"> 38 </td> <td> 2012-11-07 </td> <td align="right"> 12883.00 </td> </tr>
  <tr> <td align="right"> 39 </td> <td> 2012-11-08 </td> <td align="right"> 3219.00 </td> </tr>
  <tr> <td align="right"> 40 </td> <td> 2012-11-09 </td> <td align="right"> 10766.19 </td> </tr>
  <tr> <td align="right"> 41 </td> <td> 2012-11-10 </td> <td align="right"> 10766.19 </td> </tr>
  <tr> <td align="right"> 42 </td> <td> 2012-11-11 </td> <td align="right"> 12608.00 </td> </tr>
  <tr> <td align="right"> 43 </td> <td> 2012-11-12 </td> <td align="right"> 10765.00 </td> </tr>
  <tr> <td align="right"> 44 </td> <td> 2012-11-13 </td> <td align="right"> 7336.00 </td> </tr>
  <tr> <td align="right"> 45 </td> <td> 2012-11-14 </td> <td align="right"> 10766.19 </td> </tr>
  <tr> <td align="right"> 46 </td> <td> 2012-11-15 </td> <td align="right"> 41.00 </td> </tr>
  <tr> <td align="right"> 47 </td> <td> 2012-11-16 </td> <td align="right"> 5441.00 </td> </tr>
  <tr> <td align="right"> 48 </td> <td> 2012-11-17 </td> <td align="right"> 14339.00 </td> </tr>
  <tr> <td align="right"> 49 </td> <td> 2012-11-18 </td> <td align="right"> 15110.00 </td> </tr>
  <tr> <td align="right"> 50 </td> <td> 2012-11-19 </td> <td align="right"> 8841.00 </td> </tr>
  <tr> <td align="right"> 51 </td> <td> 2012-11-20 </td> <td align="right"> 4472.00 </td> </tr>
  <tr> <td align="right"> 52 </td> <td> 2012-11-21 </td> <td align="right"> 12787.00 </td> </tr>
  <tr> <td align="right"> 53 </td> <td> 2012-11-22 </td> <td align="right"> 20427.00 </td> </tr>
  <tr> <td align="right"> 54 </td> <td> 2012-11-23 </td> <td align="right"> 21194.00 </td> </tr>
  <tr> <td align="right"> 55 </td> <td> 2012-11-24 </td> <td align="right"> 14478.00 </td> </tr>
  <tr> <td align="right"> 56 </td> <td> 2012-11-25 </td> <td align="right"> 11834.00 </td> </tr>
  <tr> <td align="right"> 57 </td> <td> 2012-11-26 </td> <td align="right"> 11162.00 </td> </tr>
  <tr> <td align="right"> 58 </td> <td> 2012-11-27 </td> <td align="right"> 13646.00 </td> </tr>
  <tr> <td align="right"> 59 </td> <td> 2012-11-28 </td> <td align="right"> 10183.00 </td> </tr>
  <tr> <td align="right"> 60 </td> <td> 2012-11-29 </td> <td align="right"> 7047.00 </td> </tr>
  <tr> <td align="right"> 61 </td> <td> 2012-11-30 </td> <td align="right"> 10766.19 </td> </tr>
   </table>

### 4.4.2 Make a histogram of the total number of steps taken each day


```r
hist(new_total_steps_per_day$steps,
     main = "Histogram of the total number of steps taken each day",
     xlab = "Total number of steps taken each day")
```

![](PA1_template_files/figure-html/HistogramNew-1.png)<!-- -->

### 4.4.3 Calculate and report the mean and median of the total number of steps taken per day

The mean of the total number of steps taken per day is:


```r
mean(new_total_steps_per_day$steps)
```

[1] 10766.19

The median of the total number of steps taken per day is:


```r
median(new_total_steps_per_day$steps)
```

[1] 10766.19

### 4.4.4 Do these values differ from the estimates from the first part of the assignment?

The mean and median of these values are greater than the estimates from the first part of the assignment. 

            Missing     No_Missing
----------- ----------- -------------
Mean        9354.23     10766.19
Median      10395       10766.19

### 4.4.5 What is the impact of imputing missing data on the estimates of the total daily number of steps?

Imputing missing data on the estimates of the total daily number of steps will make the numbers appear greater than what they actually are.

## 5. Are there differences in activity patterns between weekdays and weekends?

### 5.1 Create a new factor variable in the dataset with two levels -- "weekday" and "weekend" indicating whether a given date is a weekday or weekend day.

### 5.1.1 Change the format of the date variable in the new_activity table

```r
new_activity$date <- as.Date(new_activity$date)
```

### 5.1.2 Create a new factor variable in the dataset with two levels -- "weekday" and "weekend"


```r
weekday <- c("Monday", "Tuesday", "Wednesday", "Thursday", "Friday")
new_activity$wkDays <- factor((weekdays(new_activity$date) %in% weekday),
                          levels = c(FALSE, TRUE), labels = c("weekend", "weekday"))

head <- xtable(head(new_activity))
print(head, type = "html")
```

<!-- html table generated in R 4.2.2 by xtable 1.8-4 package -->
<!-- Sun Jan 28 20:56:40 2024 -->
<table border=1>
<tr> <th>  </th> <th> steps </th> <th> date </th> <th> interval </th> <th> wkDays </th>  </tr>
  <tr> <td align="right"> 1 </td> <td align="right"> 37.38 </td> <td align="right"> 15614.00 </td> <td align="right">   0 </td> <td> weekday </td> </tr>
  <tr> <td align="right"> 2 </td> <td align="right"> 37.38 </td> <td align="right"> 15614.00 </td> <td align="right">   5 </td> <td> weekday </td> </tr>
  <tr> <td align="right"> 3 </td> <td align="right"> 37.38 </td> <td align="right"> 15614.00 </td> <td align="right">  10 </td> <td> weekday </td> </tr>
  <tr> <td align="right"> 4 </td> <td align="right"> 37.38 </td> <td align="right"> 15614.00 </td> <td align="right">  15 </td> <td> weekday </td> </tr>
  <tr> <td align="right"> 5 </td> <td align="right"> 37.38 </td> <td align="right"> 15614.00 </td> <td align="right">  20 </td> <td> weekday </td> </tr>
  <tr> <td align="right"> 6 </td> <td align="right"> 37.38 </td> <td align="right"> 15614.00 </td> <td align="right">  25 </td> <td> weekday </td> </tr>
   </table>

### 5.2 Make a panel plot containing a time series plot (i.e. type = "l") of the 5-minute interval (x-axis) and the average number of steps taken, averaged across all weekday days or weekend days (y-axis). See the README file in the GitHub repository to see an example of what this plot should look like using simulated data.


```r
new_activity$wkDays <- as.factor(new_activity$wkDays)

ggplot(data = new_activity, aes(x = interval, y = steps)) +
    geom_line() + 
    facet_grid(wkDays ~ .) +
    ggtitle("Panel plot of the average number of steps taken") + 
    xlab("Interval") + 
    ylab("Average number of steps taken")
```

![](PA1_template_files/figure-html/PanelPlot-1.png)<!-- -->
