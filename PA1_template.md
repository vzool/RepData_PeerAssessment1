# Reproducible Research: Peer Assessment 1

## Loading and preprocessing the data

1- Download assessement data file if it's not existed in working directory.

2- Unzip the assessement zip file(activity.zip) into the working directory.

3- load dataset file(activity.csv) into d variable.


```r

if (!file.exists("activity.zip")) {
    download.file("https://d396qusza40orc.cloudfront.net/repdata%2Fdata%2Factivity.zip", 
        destfile = "activity.zip", method = "curl")
}

if (!file.exists("activity.csv")) {
    unzip("activity.zip")
}

d <- read.csv("activity.csv", header = T)
```


## What is mean total number of steps taken per day?

```r

mean_steps <- c()
median_steps <- c()
taken_per_day <- c()
steps <- c()
interval <- c()
interval_mean <- c()
interval_median <- c()

for (a in names(table(d$date))) {
    taken_per_day <- c(taken_per_day, a)
    steps <- c(steps, sum(d[d$date %in% c(a), "steps"], na.rm = T))
    mean_steps <- c(mean_steps, mean(d[d$date %in% c(a), "steps"], na.rm = T))
    median_steps <- c(median_steps, median(d[d$date %in% c(a), "steps"], na.rm = T))
    interval <- c(interval, sum(d[d$date %in% c(a), "interval"], na.rm = T))
    interval_mean <- c(interval_mean, mean(d[d$date %in% c(a), "interval"], 
        na.rm = T))
    interval_median <- c(interval_median, median(d[d$date %in% c(a), "interval"], 
        na.rm = T))
}

steps_taken_per_day <- data.frame(day = taken_per_day, steps, mean_steps, median_steps, 
    interval, interval_mean, interval_median)

steps_taken_per_day
```

```
##           day steps mean_steps median_steps interval interval_mean
## 1  2012-10-01     0        NaN           NA   339120          1178
## 2  2012-10-02   126     0.4375            0   339120          1178
## 3  2012-10-03 11352    39.4167            0   339120          1178
## 4  2012-10-04 12116    42.0694            0   339120          1178
## 5  2012-10-05 13294    46.1597            0   339120          1178
## 6  2012-10-06 15420    53.5417            0   339120          1178
## 7  2012-10-07 11015    38.2465            0   339120          1178
## 8  2012-10-08     0        NaN           NA   339120          1178
## 9  2012-10-09 12811    44.4826            0   339120          1178
## 10 2012-10-10  9900    34.3750            0   339120          1178
## 11 2012-10-11 10304    35.7778            0   339120          1178
## 12 2012-10-12 17382    60.3542            0   339120          1178
## 13 2012-10-13 12426    43.1458            0   339120          1178
## 14 2012-10-14 15098    52.4236            0   339120          1178
## 15 2012-10-15 10139    35.2049            0   339120          1178
## 16 2012-10-16 15084    52.3750            0   339120          1178
## 17 2012-10-17 13452    46.7083            0   339120          1178
## 18 2012-10-18 10056    34.9167            0   339120          1178
## 19 2012-10-19 11829    41.0729            0   339120          1178
## 20 2012-10-20 10395    36.0938            0   339120          1178
## 21 2012-10-21  8821    30.6285            0   339120          1178
## 22 2012-10-22 13460    46.7361            0   339120          1178
## 23 2012-10-23  8918    30.9653            0   339120          1178
## 24 2012-10-24  8355    29.0104            0   339120          1178
## 25 2012-10-25  2492     8.6528            0   339120          1178
## 26 2012-10-26  6778    23.5347            0   339120          1178
## 27 2012-10-27 10119    35.1354            0   339120          1178
## 28 2012-10-28 11458    39.7847            0   339120          1178
## 29 2012-10-29  5018    17.4236            0   339120          1178
## 30 2012-10-30  9819    34.0938            0   339120          1178
## 31 2012-10-31 15414    53.5208            0   339120          1178
## 32 2012-11-01     0        NaN           NA   339120          1178
## 33 2012-11-02 10600    36.8056            0   339120          1178
## 34 2012-11-03 10571    36.7049            0   339120          1178
## 35 2012-11-04     0        NaN           NA   339120          1178
## 36 2012-11-05 10439    36.2465            0   339120          1178
## 37 2012-11-06  8334    28.9375            0   339120          1178
## 38 2012-11-07 12883    44.7326            0   339120          1178
## 39 2012-11-08  3219    11.1771            0   339120          1178
## 40 2012-11-09     0        NaN           NA   339120          1178
## 41 2012-11-10     0        NaN           NA   339120          1178
## 42 2012-11-11 12608    43.7778            0   339120          1178
## 43 2012-11-12 10765    37.3785            0   339120          1178
## 44 2012-11-13  7336    25.4722            0   339120          1178
## 45 2012-11-14     0        NaN           NA   339120          1178
## 46 2012-11-15    41     0.1424            0   339120          1178
## 47 2012-11-16  5441    18.8924            0   339120          1178
## 48 2012-11-17 14339    49.7882            0   339120          1178
## 49 2012-11-18 15110    52.4653            0   339120          1178
## 50 2012-11-19  8841    30.6979            0   339120          1178
## 51 2012-11-20  4472    15.5278            0   339120          1178
## 52 2012-11-21 12787    44.3993            0   339120          1178
## 53 2012-11-22 20427    70.9271            0   339120          1178
## 54 2012-11-23 21194    73.5903            0   339120          1178
## 55 2012-11-24 14478    50.2708            0   339120          1178
## 56 2012-11-25 11834    41.0903            0   339120          1178
## 57 2012-11-26 11162    38.7569            0   339120          1178
## 58 2012-11-27 13646    47.3819            0   339120          1178
## 59 2012-11-28 10183    35.3576            0   339120          1178
## 60 2012-11-29  7047    24.4688            0   339120          1178
## 61 2012-11-30     0        NaN           NA   339120          1178
##    interval_median
## 1             1178
## 2             1178
## 3             1178
## 4             1178
## 5             1178
## 6             1178
## 7             1178
## 8             1178
## 9             1178
## 10            1178
## 11            1178
## 12            1178
## 13            1178
## 14            1178
## 15            1178
## 16            1178
## 17            1178
## 18            1178
## 19            1178
## 20            1178
## 21            1178
## 22            1178
## 23            1178
## 24            1178
## 25            1178
## 26            1178
## 27            1178
## 28            1178
## 29            1178
## 30            1178
## 31            1178
## 32            1178
## 33            1178
## 34            1178
## 35            1178
## 36            1178
## 37            1178
## 38            1178
## 39            1178
## 40            1178
## 41            1178
## 42            1178
## 43            1178
## 44            1178
## 45            1178
## 46            1178
## 47            1178
## 48            1178
## 49            1178
## 50            1178
## 51            1178
## 52            1178
## 53            1178
## 54            1178
## 55            1178
## 56            1178
## 57            1178
## 58            1178
## 59            1178
## 60            1178
## 61            1178
```

```r

summary(steps_taken_per_day$steps)
```

```
##    Min. 1st Qu.  Median    Mean 3rd Qu.    Max. 
##       0    6780   10400    9350   12800   21200
```

```r
summary(steps_taken_per_day$mean_steps)
```

```
##    Min. 1st Qu.  Median    Mean 3rd Qu.    Max.    NA's 
##    0.14   30.70   37.40   37.40   46.20   73.60       8
```

```r
summary(steps_taken_per_day$median_steps)
```

```
##    Min. 1st Qu.  Median    Mean 3rd Qu.    Max.    NA's 
##       0       0       0       0       0       0       8
```

```r

plot.new()
hist(steps_taken_per_day$steps, main = "Steps Taken by Day", xlab = "days", 
    ylab = "steps", breaks = length(steps_taken_per_day$steps), col = rainbow(length(steps_taken_per_day$steps)))
```

![plot of chunk unnamed-chunk-2](figure/unnamed-chunk-2.png) 

```r
# hist(steps_taken_per_day$steps , main='Steps Taken by Day', xlab='days',
# ylab='steps', breaks=length(steps_taken_per_day$steps),
# col=rainbow(length(steps_taken_per_day$steps)), xaxt='n', yaxt='n')
# axis(side=1, at=steps_taken_per_day$steps, labels=steps_taken_per_day$day)

# axis at at <- c() for(i in 0:5){ at <- c(at,
# (round(length(steps_taken_per_day$steps)/5)*i)) } labels <-
# round(seq(from=min(steps_taken_per_day$steps),
# to=max(steps_taken_per_day$steps), length.out=6)) axis(side=2, at=at,
# labels=labels)
```



## What is the average daily activity pattern?

```r
plot(steps_taken_per_day$mean_steps, type = "l", xlab = "days", ylab = "average daily activity")
```

![plot of chunk unnamed-chunk-3](figure/unnamed-chunk-3.png) 


## Imputing missing values

```r

missings_count <- nrow(d[is.na(d$steps), ])

print(paste("Total number of rows with NAs: ", missings_count))
```

```
## [1] "Total number of rows with NAs:  2304"
```

```r

data_with_missings_filled <- d

data_with_missings_filled[is.na(data_with_missings_filled$steps), "steps"] <- seq(missings_count)


########################################################## 
mean_steps <- c()
median_steps <- c()
taken_per_day <- c()
steps <- c()
interval <- c()

for (a in names(table(data_with_missings_filled$date))) {
    taken_per_day <- c(taken_per_day, a)
    steps <- c(steps, sum(data_with_missings_filled[data_with_missings_filled$date %in% 
        c(a), "steps"], na.rm = T))
    mean_steps <- c(mean_steps, mean(data_with_missings_filled[data_with_missings_filled$date %in% 
        c(a), "steps"], na.rm = T))
    median_steps <- c(median_steps, median(data_with_missings_filled[data_with_missings_filled$date %in% 
        c(a), "steps"], na.rm = T))
    interval <- c(interval, sum(data_with_missings_filled[data_with_missings_filled$date %in% 
        c(a), "interval"], na.rm = T))
}

missings_filled_per_day <- data.frame(day = taken_per_day, steps, mean_steps, 
    median_steps, interval)

missings_filled_per_day
```

```
##           day  steps mean_steps median_steps interval
## 1  2012-10-01  41616   144.5000        144.5   339120
## 2  2012-10-02    126     0.4375          0.0   339120
## 3  2012-10-03  11352    39.4167          0.0   339120
## 4  2012-10-04  12116    42.0694          0.0   339120
## 5  2012-10-05  13294    46.1597          0.0   339120
## 6  2012-10-06  15420    53.5417          0.0   339120
## 7  2012-10-07  11015    38.2465          0.0   339120
## 8  2012-10-08 124560   432.5000        432.5   339120
## 9  2012-10-09  12811    44.4826          0.0   339120
## 10 2012-10-10   9900    34.3750          0.0   339120
## 11 2012-10-11  10304    35.7778          0.0   339120
## 12 2012-10-12  17382    60.3542          0.0   339120
## 13 2012-10-13  12426    43.1458          0.0   339120
## 14 2012-10-14  15098    52.4236          0.0   339120
## 15 2012-10-15  10139    35.2049          0.0   339120
## 16 2012-10-16  15084    52.3750          0.0   339120
## 17 2012-10-17  13452    46.7083          0.0   339120
## 18 2012-10-18  10056    34.9167          0.0   339120
## 19 2012-10-19  11829    41.0729          0.0   339120
## 20 2012-10-20  10395    36.0938          0.0   339120
## 21 2012-10-21   8821    30.6285          0.0   339120
## 22 2012-10-22  13460    46.7361          0.0   339120
## 23 2012-10-23   8918    30.9653          0.0   339120
## 24 2012-10-24   8355    29.0104          0.0   339120
## 25 2012-10-25   2492     8.6528          0.0   339120
## 26 2012-10-26   6778    23.5347          0.0   339120
## 27 2012-10-27  10119    35.1354          0.0   339120
## 28 2012-10-28  11458    39.7847          0.0   339120
## 29 2012-10-29   5018    17.4236          0.0   339120
## 30 2012-10-30   9819    34.0938          0.0   339120
## 31 2012-10-31  15414    53.5208          0.0   339120
## 32 2012-11-01 207504   720.5000        720.5   339120
## 33 2012-11-02  10600    36.8056          0.0   339120
## 34 2012-11-03  10571    36.7049          0.0   339120
## 35 2012-11-04 290448  1008.5000       1008.5   339120
## 36 2012-11-05  10439    36.2465          0.0   339120
## 37 2012-11-06   8334    28.9375          0.0   339120
## 38 2012-11-07  12883    44.7326          0.0   339120
## 39 2012-11-08   3219    11.1771          0.0   339120
## 40 2012-11-09 373392  1296.5000       1296.5   339120
## 41 2012-11-10 456336  1584.5000       1584.5   339120
## 42 2012-11-11  12608    43.7778          0.0   339120
## 43 2012-11-12  10765    37.3785          0.0   339120
## 44 2012-11-13   7336    25.4722          0.0   339120
## 45 2012-11-14 539280  1872.5000       1872.5   339120
## 46 2012-11-15     41     0.1424          0.0   339120
## 47 2012-11-16   5441    18.8924          0.0   339120
## 48 2012-11-17  14339    49.7882          0.0   339120
## 49 2012-11-18  15110    52.4653          0.0   339120
## 50 2012-11-19   8841    30.6979          0.0   339120
## 51 2012-11-20   4472    15.5278          0.0   339120
## 52 2012-11-21  12787    44.3993          0.0   339120
## 53 2012-11-22  20427    70.9271          0.0   339120
## 54 2012-11-23  21194    73.5903          0.0   339120
## 55 2012-11-24  14478    50.2708          0.0   339120
## 56 2012-11-25  11834    41.0903          0.0   339120
## 57 2012-11-26  11162    38.7569          0.0   339120
## 58 2012-11-27  13646    47.3819          0.0   339120
## 59 2012-11-28  10183    35.3576          0.0   339120
## 60 2012-11-29   7047    24.4688          0.0   339120
## 61 2012-11-30 622224  2160.5000       2160.5   339120
```

```r

summary(missings_filled_per_day)
```

```
##          day         steps          mean_steps      median_steps 
##  2012-10-01: 1   Min.   :    41   Min.   :   0.1   Min.   :   0  
##  2012-10-02: 1   1st Qu.:  9819   1st Qu.:  34.1   1st Qu.:   0  
##  2012-10-03: 1   Median : 11458   Median :  39.8   Median :   0  
##  2012-10-04: 1   Mean   : 52885   Mean   : 183.6   Mean   : 151  
##  2012-10-05: 1   3rd Qu.: 15084   3rd Qu.:  52.4   3rd Qu.:   0  
##  2012-10-06: 1   Max.   :622224   Max.   :2160.5   Max.   :2160  
##  (Other)   :55                                                   
##     interval     
##  Min.   :339120  
##  1st Qu.:339120  
##  Median :339120  
##  Mean   :339120  
##  3rd Qu.:339120  
##  Max.   :339120  
## 
```

```r

########################################################## 

hist(data_with_missings_filled$steps)
```

![plot of chunk unnamed-chunk-4](figure/unnamed-chunk-4.png) 



## Are there differences in activity patterns between weekdays and weekends?

```r

missings_filled_per_day$weekday_weekend <- weekdays(as.Date(missings_filled_per_day$day, 
    "%Y-%m-%d")) %in% c("Sunday")

missings_filled_per_day[missings_filled_per_day$weekday_weekend, "weekday_weekend"] <- "weekend"
missings_filled_per_day[missings_filled_per_day$weekday_weekend == F, "weekday_weekend"] <- "weekday"

missings_filled_per_day
```

```
##           day  steps mean_steps median_steps interval weekday_weekend
## 1  2012-10-01  41616   144.5000        144.5   339120         weekday
## 2  2012-10-02    126     0.4375          0.0   339120         weekday
## 3  2012-10-03  11352    39.4167          0.0   339120         weekday
## 4  2012-10-04  12116    42.0694          0.0   339120         weekday
## 5  2012-10-05  13294    46.1597          0.0   339120         weekday
## 6  2012-10-06  15420    53.5417          0.0   339120         weekday
## 7  2012-10-07  11015    38.2465          0.0   339120         weekend
## 8  2012-10-08 124560   432.5000        432.5   339120         weekday
## 9  2012-10-09  12811    44.4826          0.0   339120         weekday
## 10 2012-10-10   9900    34.3750          0.0   339120         weekday
## 11 2012-10-11  10304    35.7778          0.0   339120         weekday
## 12 2012-10-12  17382    60.3542          0.0   339120         weekday
## 13 2012-10-13  12426    43.1458          0.0   339120         weekday
## 14 2012-10-14  15098    52.4236          0.0   339120         weekend
## 15 2012-10-15  10139    35.2049          0.0   339120         weekday
## 16 2012-10-16  15084    52.3750          0.0   339120         weekday
## 17 2012-10-17  13452    46.7083          0.0   339120         weekday
## 18 2012-10-18  10056    34.9167          0.0   339120         weekday
## 19 2012-10-19  11829    41.0729          0.0   339120         weekday
## 20 2012-10-20  10395    36.0938          0.0   339120         weekday
## 21 2012-10-21   8821    30.6285          0.0   339120         weekend
## 22 2012-10-22  13460    46.7361          0.0   339120         weekday
## 23 2012-10-23   8918    30.9653          0.0   339120         weekday
## 24 2012-10-24   8355    29.0104          0.0   339120         weekday
## 25 2012-10-25   2492     8.6528          0.0   339120         weekday
## 26 2012-10-26   6778    23.5347          0.0   339120         weekday
## 27 2012-10-27  10119    35.1354          0.0   339120         weekday
## 28 2012-10-28  11458    39.7847          0.0   339120         weekend
## 29 2012-10-29   5018    17.4236          0.0   339120         weekday
## 30 2012-10-30   9819    34.0938          0.0   339120         weekday
## 31 2012-10-31  15414    53.5208          0.0   339120         weekday
## 32 2012-11-01 207504   720.5000        720.5   339120         weekday
## 33 2012-11-02  10600    36.8056          0.0   339120         weekday
## 34 2012-11-03  10571    36.7049          0.0   339120         weekday
## 35 2012-11-04 290448  1008.5000       1008.5   339120         weekend
## 36 2012-11-05  10439    36.2465          0.0   339120         weekday
## 37 2012-11-06   8334    28.9375          0.0   339120         weekday
## 38 2012-11-07  12883    44.7326          0.0   339120         weekday
## 39 2012-11-08   3219    11.1771          0.0   339120         weekday
## 40 2012-11-09 373392  1296.5000       1296.5   339120         weekday
## 41 2012-11-10 456336  1584.5000       1584.5   339120         weekday
## 42 2012-11-11  12608    43.7778          0.0   339120         weekend
## 43 2012-11-12  10765    37.3785          0.0   339120         weekday
## 44 2012-11-13   7336    25.4722          0.0   339120         weekday
## 45 2012-11-14 539280  1872.5000       1872.5   339120         weekday
## 46 2012-11-15     41     0.1424          0.0   339120         weekday
## 47 2012-11-16   5441    18.8924          0.0   339120         weekday
## 48 2012-11-17  14339    49.7882          0.0   339120         weekday
## 49 2012-11-18  15110    52.4653          0.0   339120         weekend
## 50 2012-11-19   8841    30.6979          0.0   339120         weekday
## 51 2012-11-20   4472    15.5278          0.0   339120         weekday
## 52 2012-11-21  12787    44.3993          0.0   339120         weekday
## 53 2012-11-22  20427    70.9271          0.0   339120         weekday
## 54 2012-11-23  21194    73.5903          0.0   339120         weekday
## 55 2012-11-24  14478    50.2708          0.0   339120         weekday
## 56 2012-11-25  11834    41.0903          0.0   339120         weekend
## 57 2012-11-26  11162    38.7569          0.0   339120         weekday
## 58 2012-11-27  13646    47.3819          0.0   339120         weekday
## 59 2012-11-28  10183    35.3576          0.0   339120         weekday
## 60 2012-11-29   7047    24.4688          0.0   339120         weekday
## 61 2012-11-30 622224  2160.5000       2160.5   339120         weekday
```

```r

plot.new()
plot(missings_filled_per_day[missings_filled_per_day$weekday_weekend == "weekend", 
    "steps"], type = "l", main = "weekend")
```

![plot of chunk unnamed-chunk-5](figure/unnamed-chunk-51.png) 

```r
plot(missings_filled_per_day[missings_filled_per_day$weekday_weekend == "weekday", 
    "steps"], type = "l", main = "weekday")
```

![plot of chunk unnamed-chunk-5](figure/unnamed-chunk-52.png) 


