Working with Activity Data
==========================

Kenney Snell

Introduction
------------

1. Code for reading in the dataset and/or processing the data
=============================================================

    setwd("C:\\Users\\app1kms\\Documents\\Training\\2017\\DataScience_Downloads\\Reproducibe_Research\\repdata%2Fdata%2Factivity")
    act_df  <- read.csv("activity.csv")
    str(act_df)

    ## 'data.frame':    17568 obs. of  3 variables:
    ##  $ steps   : int  NA NA NA NA NA NA NA NA NA NA ...
    ##  $ date    : Factor w/ 61 levels "2012-10-01","2012-10-02",..: 1 1 1 1 1 1 1 1 1 1 ...
    ##  $ interval: int  0 5 10 15 20 25 30 35 40 45 ...

    summary(act_df)

    ##      steps                date          interval     
    ##  Min.   :  0.00   2012-10-01:  288   Min.   :   0.0  
    ##  1st Qu.:  0.00   2012-10-02:  288   1st Qu.: 588.8  
    ##  Median :  0.00   2012-10-03:  288   Median :1177.5  
    ##  Mean   : 37.38   2012-10-04:  288   Mean   :1177.5  
    ##  3rd Qu.: 12.00   2012-10-05:  288   3rd Qu.:1766.2  
    ##  Max.   :806.00   2012-10-06:  288   Max.   :2355.0  
    ##  NA's   :2304     (Other)   :15840

Process and transform the data

    activity_cpl <- act_df[complete.cases(act_df),]
    str(activity_cpl)

    ## 'data.frame':    15264 obs. of  3 variables:
    ##  $ steps   : int  0 0 0 0 0 0 0 0 0 0 ...
    ##  $ date    : Factor w/ 61 levels "2012-10-01","2012-10-02",..: 2 2 2 2 2 2 2 2 2 2 ...
    ##  $ interval: int  0 5 10 15 20 25 30 35 40 45 ...

    summary(activity_cpl)

    ##      steps                date          interval     
    ##  Min.   :  0.00   2012-10-02:  288   Min.   :   0.0  
    ##  1st Qu.:  0.00   2012-10-03:  288   1st Qu.: 588.8  
    ##  Median :  0.00   2012-10-04:  288   Median :1177.5  
    ##  Mean   : 37.38   2012-10-05:  288   Mean   :1177.5  
    ##  3rd Qu.: 12.00   2012-10-06:  288   3rd Qu.:1766.2  
    ##  Max.   :806.00   2012-10-07:  288   Max.   :2355.0  
    ##                   (Other)   :13536

2. Make a histogram of the total number of steps taken each day
===============================================================

Calculate the total number of steps taken per day

    histData <-  aggregate(steps ~ date, data = activity_cpl, sum)
    steps <- histData

The total number of steps taken for each day is:

    steps

    ##          date steps
    ## 1  2012-10-02   126
    ## 2  2012-10-03 11352
    ## 3  2012-10-04 12116
    ## 4  2012-10-05 13294
    ## 5  2012-10-06 15420
    ## 6  2012-10-07 11015
    ## 7  2012-10-09 12811
    ## 8  2012-10-10  9900
    ## 9  2012-10-11 10304
    ## 10 2012-10-12 17382
    ## 11 2012-10-13 12426
    ## 12 2012-10-14 15098
    ## 13 2012-10-15 10139
    ## 14 2012-10-16 15084
    ## 15 2012-10-17 13452
    ## 16 2012-10-18 10056
    ## 17 2012-10-19 11829
    ## 18 2012-10-20 10395
    ## 19 2012-10-21  8821
    ## 20 2012-10-22 13460
    ## 21 2012-10-23  8918
    ## 22 2012-10-24  8355
    ## 23 2012-10-25  2492
    ## 24 2012-10-26  6778
    ## 25 2012-10-27 10119
    ## 26 2012-10-28 11458
    ## 27 2012-10-29  5018
    ## 28 2012-10-30  9819
    ## 29 2012-10-31 15414
    ## 30 2012-11-02 10600
    ## 31 2012-11-03 10571
    ## 32 2012-11-05 10439
    ## 33 2012-11-06  8334
    ## 34 2012-11-07 12883
    ## 35 2012-11-08  3219
    ## 36 2012-11-11 12608
    ## 37 2012-11-12 10765
    ## 38 2012-11-13  7336
    ## 39 2012-11-15    41
    ## 40 2012-11-16  5441
    ## 41 2012-11-17 14339
    ## 42 2012-11-18 15110
    ## 43 2012-11-19  8841
    ## 44 2012-11-20  4472
    ## 45 2012-11-21 12787
    ## 46 2012-11-22 20427
    ## 47 2012-11-23 21194
    ## 48 2012-11-24 14478
    ## 49 2012-11-25 11834
    ## 50 2012-11-26 11162
    ## 51 2012-11-27 13646
    ## 52 2012-11-28 10183
    ## 53 2012-11-29  7047

    h <- hist(histData$steps,  # Save histogram as object
              breaks = 11,  # "Suggests" 11 bins for the histogram
              freq = T,
              col = "thistle1", 
              main = "Histogram of Activity",
              xlab = "Number of daily steps")

![](PA1_template_files/figure-markdown_strict/plot2-1.png)

3. Calculate and report the mean and median of the total number of steps taken per day
======================================================================================

    Mean_steps <- mean(histData$steps)
    Median_steps <- median(histData$steps)

The mean of the toal number of steps per day is 1.076618910^{4}. The
median of the toal number of steps per day is 10765.

4. Time series plot of the average number of steps taken
========================================================

Make a time series plot (i.e. type = "l") of the 5-minute interval
(x-axis) and the average number of steps taken, averaged across all days
(y-axis)

    histData <-  aggregate(steps ~ date, data = activity_cpl, sum)
    Median_steps <- median(histData$steps)


    PlotData <-  aggregate(steps ~ interval, data = activity_cpl, mean)



    plot(PlotData$steps ~ interval, PlotData, xaxt = "n", type = "l")
    axis(1, PlotData$interval,  cex.axis = .7)

![](PA1_template_files/figure-markdown_strict/plot4-1.png)

5. The 5-minute interval that, on average, contains the maximum number of steps
===============================================================================

    maxSteps = max(PlotData$steps)
    library(dplyr)

    Maxinterval <- subset(PlotData, steps==maxSteps,select=interval)

    Maxinterval

    ##     interval
    ## 104      835

The max interval is 835, for a value of 206.1698113.

6.Code to describe and show a strategy for imputing missing data
================================================================

    for (Var in names(act_df)) {
        missing <- sum(is.na(act_df[,Var]))
        if (missing > 0) {
           missing_steps <-  print(c(Var,missing))
        }
    }

    ## [1] "steps" "2304"

The total number of missing rows is steps, 2304. \# 7. Histogram of the
total number of steps taken each day after missing values are imputed

Assign the mean of that interval for missing values

    MeanData <-  aggregate(steps ~ interval, data = activity_cpl, mean)

    # new Data Frame
    act_df2 <- act_df

    for (i in as.numeric(1: nrow(act_df))) {
        
        if(is.na(act_df[i,1]))  {
       
       
        MeanStep <- subset(MeanData, interval==act_df$interval[i],select=steps)
        
        act_df2[i,1] <- MeanStep

          }
         
        
        }

Use the new updated data frame

    histDataNew <-  aggregate(steps ~ date, data = act_df2, sum)
    stepsNew <- histDataNew
    h <- hist(histDataNew$steps,  # Save histogram as object
              breaks = 11,  # "Suggests" 11 bins for the histogram
              freq = T,
              col = "thistle1", 
              main = "Histogram of Activity",
              xlab = "Number of daily steps")

![](PA1_template_files/figure-markdown_strict/unnamed-chunk-9-1.png)

Calculate the NEW mean and median

    Mean_stepsNew <- mean(histDataNew$steps)
    Median_stepsNew <- median(histDataNew$steps)

The NEW mean of the toal number of steps per day is 1.076618910^{4}. The
NEW median of the toal number of steps per day is 1.076618910^{4}.

The ORIGINAL mean of the toal number of steps per day is
1.076618910^{4}. The ORIGINAL median of the toal number of steps per day
is 10765.

Result are that the mean didn't vhange becuase of using the overal mean
of each interval. But the median was slightly less.

8. Panel plot comparing the average number of steps taken per 5-minute interval across weekdays and weekends
============================================================================================================

1.  Create a new factor variable in the dataset with two levels -
    "weekday" and "weekend" indicating whether a given date is a weekday
    or weekend day.

<!-- -->

    act_df2$weekday <- weekdays(as.Date(act_df2$date))
    act_df2$date <- as.Date(act_df2$date)
    weekdays1 <- c('Monday', 'Tuesday', 'Wednesday', 'Thursday', 'Friday')

    #Use `%in%` and `weekdays` to create a logical vector
    #convert to `factor` and specify the `levels/labels`

    act_df2$wday <- factor((weekdays(act_df2$date) %in% weekdays1), 
             levels=c(FALSE, TRUE), labels=c('weekend', 'weekday')
    )
    act_df2

    ##             steps       date interval   weekday    wday
    ## 1       1.7169811 2012-10-01        0    Monday weekday
    ## 2       0.3396226 2012-10-01        5    Monday weekday
    ## 3       0.1320755 2012-10-01       10    Monday weekday
    ## 4       0.1509434 2012-10-01       15    Monday weekday
    ## 5       0.0754717 2012-10-01       20    Monday weekday
    ## 6       2.0943396 2012-10-01       25    Monday weekday
    ## 7       0.5283019 2012-10-01       30    Monday weekday
    ## 8       0.8679245 2012-10-01       35    Monday weekday
    ## 9       0.0000000 2012-10-01       40    Monday weekday
    ## 10      1.4716981 2012-10-01       45    Monday weekday
    ## 11      0.3018868 2012-10-01       50    Monday weekday
    ## 12      0.1320755 2012-10-01       55    Monday weekday
    ## 13      0.3207547 2012-10-01      100    Monday weekday
    ## 14      0.6792453 2012-10-01      105    Monday weekday
    ## 15      0.1509434 2012-10-01      110    Monday weekday
    ## 16      0.3396226 2012-10-01      115    Monday weekday
    ## 17      0.0000000 2012-10-01      120    Monday weekday
    ## 18      1.1132075 2012-10-01      125    Monday weekday
    ## 19      1.8301887 2012-10-01      130    Monday weekday
    ## 20      0.1698113 2012-10-01      135    Monday weekday
    ## 21      0.1698113 2012-10-01      140    Monday weekday
    ## 22      0.3773585 2012-10-01      145    Monday weekday
    ## 23      0.2641509 2012-10-01      150    Monday weekday
    ## 24      0.0000000 2012-10-01      155    Monday weekday
    ## 25      0.0000000 2012-10-01      200    Monday weekday
    ## 26      0.0000000 2012-10-01      205    Monday weekday
    ## 27      1.1320755 2012-10-01      210    Monday weekday
    ## 28      0.0000000 2012-10-01      215    Monday weekday
    ## 29      0.0000000 2012-10-01      220    Monday weekday
    ## 30      0.1320755 2012-10-01      225    Monday weekday
    ## 31      0.0000000 2012-10-01      230    Monday weekday
    ## 32      0.2264151 2012-10-01      235    Monday weekday
    ## 33      0.0000000 2012-10-01      240    Monday weekday
    ## 34      0.0000000 2012-10-01      245    Monday weekday
    ## 35      1.5471698 2012-10-01      250    Monday weekday
    ## 36      0.9433962 2012-10-01      255    Monday weekday
    ## 37      0.0000000 2012-10-01      300    Monday weekday
    ## 38      0.0000000 2012-10-01      305    Monday weekday
    ## 39      0.0000000 2012-10-01      310    Monday weekday
    ## 40      0.0000000 2012-10-01      315    Monday weekday
    ## 41      0.2075472 2012-10-01      320    Monday weekday
    ## 42      0.6226415 2012-10-01      325    Monday weekday
    ## 43      1.6226415 2012-10-01      330    Monday weekday
    ## 44      0.5849057 2012-10-01      335    Monday weekday
    ## 45      0.4905660 2012-10-01      340    Monday weekday
    ## 46      0.0754717 2012-10-01      345    Monday weekday
    ## 47      0.0000000 2012-10-01      350    Monday weekday
    ## 48      0.0000000 2012-10-01      355    Monday weekday
    ## 49      1.1886792 2012-10-01      400    Monday weekday
    ## 50      0.9433962 2012-10-01      405    Monday weekday
    ## 51      2.5660377 2012-10-01      410    Monday weekday
    ## 52      0.0000000 2012-10-01      415    Monday weekday
    ## 53      0.3396226 2012-10-01      420    Monday weekday
    ## 54      0.3584906 2012-10-01      425    Monday weekday
    ## 55      4.1132075 2012-10-01      430    Monday weekday
    ## 56      0.6603774 2012-10-01      435    Monday weekday
    ## 57      3.4905660 2012-10-01      440    Monday weekday
    ## 58      0.8301887 2012-10-01      445    Monday weekday
    ## 59      3.1132075 2012-10-01      450    Monday weekday
    ## 60      1.1132075 2012-10-01      455    Monday weekday
    ## 61      0.0000000 2012-10-01      500    Monday weekday
    ## 62      1.5660377 2012-10-01      505    Monday weekday
    ## 63      3.0000000 2012-10-01      510    Monday weekday
    ## 64      2.2452830 2012-10-01      515    Monday weekday
    ## 65      3.3207547 2012-10-01      520    Monday weekday
    ## 66      2.9622642 2012-10-01      525    Monday weekday
    ## 67      2.0943396 2012-10-01      530    Monday weekday
    ## 68      6.0566038 2012-10-01      535    Monday weekday
    ## 69     16.0188679 2012-10-01      540    Monday weekday
    ## 70     18.3396226 2012-10-01      545    Monday weekday
    ## 71     39.4528302 2012-10-01      550    Monday weekday
    ## 72     44.4905660 2012-10-01      555    Monday weekday
    ## 73     31.4905660 2012-10-01      600    Monday weekday
    ## 74     49.2641509 2012-10-01      605    Monday weekday
    ## 75     53.7735849 2012-10-01      610    Monday weekday
    ## 76     63.4528302 2012-10-01      615    Monday weekday
    ## 77     49.9622642 2012-10-01      620    Monday weekday
    ## 78     47.0754717 2012-10-01      625    Monday weekday
    ## 79     52.1509434 2012-10-01      630    Monday weekday
    ## 80     39.3396226 2012-10-01      635    Monday weekday
    ## 81     44.0188679 2012-10-01      640    Monday weekday
    ## 82     44.1698113 2012-10-01      645    Monday weekday
    ## 83     37.3584906 2012-10-01      650    Monday weekday
    ## 84     49.0377358 2012-10-01      655    Monday weekday
    ## 85     43.8113208 2012-10-01      700    Monday weekday
    ## 86     44.3773585 2012-10-01      705    Monday weekday
    ## 87     50.5094340 2012-10-01      710    Monday weekday
    ## 88     54.5094340 2012-10-01      715    Monday weekday
    ## 89     49.9245283 2012-10-01      720    Monday weekday
    ## 90     50.9811321 2012-10-01      725    Monday weekday
    ## 91     55.6792453 2012-10-01      730    Monday weekday
    ## 92     44.3207547 2012-10-01      735    Monday weekday
    ## 93     52.2641509 2012-10-01      740    Monday weekday
    ## 94     69.5471698 2012-10-01      745    Monday weekday
    ## 95     57.8490566 2012-10-01      750    Monday weekday
    ## 96     56.1509434 2012-10-01      755    Monday weekday
    ## 97     73.3773585 2012-10-01      800    Monday weekday
    ## 98     68.2075472 2012-10-01      805    Monday weekday
    ## 99    129.4339623 2012-10-01      810    Monday weekday
    ## 100   157.5283019 2012-10-01      815    Monday weekday
    ## 101   171.1509434 2012-10-01      820    Monday weekday
    ## 102   155.3962264 2012-10-01      825    Monday weekday
    ## 103   177.3018868 2012-10-01      830    Monday weekday
    ## 104   206.1698113 2012-10-01      835    Monday weekday
    ## 105   195.9245283 2012-10-01      840    Monday weekday
    ## 106   179.5660377 2012-10-01      845    Monday weekday
    ## 107   183.3962264 2012-10-01      850    Monday weekday
    ## 108   167.0188679 2012-10-01      855    Monday weekday
    ## 109   143.4528302 2012-10-01      900    Monday weekday
    ## 110   124.0377358 2012-10-01      905    Monday weekday
    ## 111   109.1132075 2012-10-01      910    Monday weekday
    ## 112   108.1132075 2012-10-01      915    Monday weekday
    ## 113   103.7169811 2012-10-01      920    Monday weekday
    ## 114    95.9622642 2012-10-01      925    Monday weekday
    ## 115    66.2075472 2012-10-01      930    Monday weekday
    ## 116    45.2264151 2012-10-01      935    Monday weekday
    ## 117    24.7924528 2012-10-01      940    Monday weekday
    ## 118    38.7547170 2012-10-01      945    Monday weekday
    ## 119    34.9811321 2012-10-01      950    Monday weekday
    ## 120    21.0566038 2012-10-01      955    Monday weekday
    ## 121    40.5660377 2012-10-01     1000    Monday weekday
    ## 122    26.9811321 2012-10-01     1005    Monday weekday
    ## 123    42.4150943 2012-10-01     1010    Monday weekday
    ## 124    52.6603774 2012-10-01     1015    Monday weekday
    ## 125    38.9245283 2012-10-01     1020    Monday weekday
    ## 126    50.7924528 2012-10-01     1025    Monday weekday
    ## 127    44.2830189 2012-10-01     1030    Monday weekday
    ## 128    37.4150943 2012-10-01     1035    Monday weekday
    ## 129    34.6981132 2012-10-01     1040    Monday weekday
    ## 130    28.3396226 2012-10-01     1045    Monday weekday
    ## 131    25.0943396 2012-10-01     1050    Monday weekday
    ## 132    31.9433962 2012-10-01     1055    Monday weekday
    ## 133    31.3584906 2012-10-01     1100    Monday weekday
    ## 134    29.6792453 2012-10-01     1105    Monday weekday
    ## 135    21.3207547 2012-10-01     1110    Monday weekday
    ## 136    25.5471698 2012-10-01     1115    Monday weekday
    ## 137    28.3773585 2012-10-01     1120    Monday weekday
    ## 138    26.4716981 2012-10-01     1125    Monday weekday
    ## 139    33.4339623 2012-10-01     1130    Monday weekday
    ## 140    49.9811321 2012-10-01     1135    Monday weekday
    ## 141    42.0377358 2012-10-01     1140    Monday weekday
    ## 142    44.6037736 2012-10-01     1145    Monday weekday
    ## 143    46.0377358 2012-10-01     1150    Monday weekday
    ## 144    59.1886792 2012-10-01     1155    Monday weekday
    ## 145    63.8679245 2012-10-01     1200    Monday weekday
    ## 146    87.6981132 2012-10-01     1205    Monday weekday
    ## 147    94.8490566 2012-10-01     1210    Monday weekday
    ## 148    92.7735849 2012-10-01     1215    Monday weekday
    ## 149    63.3962264 2012-10-01     1220    Monday weekday
    ## 150    50.1698113 2012-10-01     1225    Monday weekday
    ## 151    54.4716981 2012-10-01     1230    Monday weekday
    ## 152    32.4150943 2012-10-01     1235    Monday weekday
    ## 153    26.5283019 2012-10-01     1240    Monday weekday
    ## 154    37.7358491 2012-10-01     1245    Monday weekday
    ## 155    45.0566038 2012-10-01     1250    Monday weekday
    ## 156    67.2830189 2012-10-01     1255    Monday weekday
    ## 157    42.3396226 2012-10-01     1300    Monday weekday
    ## 158    39.8867925 2012-10-01     1305    Monday weekday
    ## 159    43.2641509 2012-10-01     1310    Monday weekday
    ## 160    40.9811321 2012-10-01     1315    Monday weekday
    ## 161    46.2452830 2012-10-01     1320    Monday weekday
    ## 162    56.4339623 2012-10-01     1325    Monday weekday
    ## 163    42.7547170 2012-10-01     1330    Monday weekday
    ## 164    25.1320755 2012-10-01     1335    Monday weekday
    ## 165    39.9622642 2012-10-01     1340    Monday weekday
    ## 166    53.5471698 2012-10-01     1345    Monday weekday
    ## 167    47.3207547 2012-10-01     1350    Monday weekday
    ## 168    60.8113208 2012-10-01     1355    Monday weekday
    ## 169    55.7547170 2012-10-01     1400    Monday weekday
    ## 170    51.9622642 2012-10-01     1405    Monday weekday
    ## 171    43.5849057 2012-10-01     1410    Monday weekday
    ## 172    48.6981132 2012-10-01     1415    Monday weekday
    ## 173    35.4716981 2012-10-01     1420    Monday weekday
    ## 174    37.5471698 2012-10-01     1425    Monday weekday
    ## 175    41.8490566 2012-10-01     1430    Monday weekday
    ## 176    27.5094340 2012-10-01     1435    Monday weekday
    ## 177    17.1132075 2012-10-01     1440    Monday weekday
    ## 178    26.0754717 2012-10-01     1445    Monday weekday
    ## 179    43.6226415 2012-10-01     1450    Monday weekday
    ## 180    43.7735849 2012-10-01     1455    Monday weekday
    ## 181    30.0188679 2012-10-01     1500    Monday weekday
    ## 182    36.0754717 2012-10-01     1505    Monday weekday
    ## 183    35.4905660 2012-10-01     1510    Monday weekday
    ## 184    38.8490566 2012-10-01     1515    Monday weekday
    ## 185    45.9622642 2012-10-01     1520    Monday weekday
    ## 186    47.7547170 2012-10-01     1525    Monday weekday
    ## 187    48.1320755 2012-10-01     1530    Monday weekday
    ## 188    65.3207547 2012-10-01     1535    Monday weekday
    ## 189    82.9056604 2012-10-01     1540    Monday weekday
    ## 190    98.6603774 2012-10-01     1545    Monday weekday
    ## 191   102.1132075 2012-10-01     1550    Monday weekday
    ## 192    83.9622642 2012-10-01     1555    Monday weekday
    ## 193    62.1320755 2012-10-01     1600    Monday weekday
    ## 194    64.1320755 2012-10-01     1605    Monday weekday
    ## 195    74.5471698 2012-10-01     1610    Monday weekday
    ## 196    63.1698113 2012-10-01     1615    Monday weekday
    ## 197    56.9056604 2012-10-01     1620    Monday weekday
    ## 198    59.7735849 2012-10-01     1625    Monday weekday
    ## 199    43.8679245 2012-10-01     1630    Monday weekday
    ## 200    38.5660377 2012-10-01     1635    Monday weekday
    ##  [ reached getOption("max.print") -- omitted 17368 rows ]

New plot for Weekday and weekend

     # create table with steps per time across weekdaydays or weekend days
     StepsPerTimeDT <- aggregate(steps~interval+wday,data=act_df2,FUN=mean,na.action=na.omit)
     # variable time (more comprensible for the graph axis)
     
     # draw the line plot
    library(ggplot2)
     j <- ggplot(StepsPerTimeDT, aes(interval, steps))
     j+geom_line(col="blue")+ggtitle("Average steps per 5 minute interval: weekdays vs. weekends")+xlab("Interval")+ylab("Steps")+theme(plot.title = element_text(face="bold", size=12))+facet_grid(wday ~ .)

![](PA1_template_files/figure-markdown_strict/timeplot2-1.png)

############### 

R Markdown
----------

This is an R Markdown document. Markdown is a simple formatting syntax
for authoring HTML, PDF, and MS Word documents. For more details on
using R Markdown see <http://rmarkdown.rstudio.com>.

When you click the **Knit** button a document will be generated that
includes both content as well as the output of any embedded R code
chunks within the document. You can embed an R code chunk like this:
