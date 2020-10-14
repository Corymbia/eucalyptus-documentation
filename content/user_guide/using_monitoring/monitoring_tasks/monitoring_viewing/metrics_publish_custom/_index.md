+++
title = "Publish Custom Metrics"
weight = 30
+++

CloudWatch allows you to publish your own metrics, such as application performance, system health, or customer usage.
## Publish a single data point
To publish a single data point for a new or existing metric, call euwatch-put-data with one value and time stamp. For example, the following actions each publish one data point: 



    euwatch-put-data --metric-name PageViewCount --namespace "TestService" --value 2 --timestamp 2011-03-14T12:00:00.000Z
    euwatch-put-data --metric-name PageViewCount --namespace "TestService" --value 4 --timestamp 2011-03-14T12:00:01.000Z
    euwatch-put-data --metric-name PageViewCount --namespace "TestService" --value 5 --timestamp 2011-03-14T12:00:02.000Z

You can publish data points with time stamps as granular as one-thousandth of a second. However, CloudWatch aggregates the data to a minimum granularity of 60 seconds. For example, the `PageViewCount` metric from the previous examples contains three data points with time stamps just seconds apart. CloudWatch aggregates the three data points because they all have time stamps within a 60-second period. 

CloudWatch uses 60-second boundaries when aggregating data points. For example, CloudWatch aggregates the data points from the previous example because all three data points fall within the 60-second period that begins at 2011-03-14T12:00:00.000Z and ends at 2011-03-14T12:00:59.999Z. 


## Publish statistic sets
You can also aggregate your data before you publish to CloudWatch. When you have multiple data points per minute, aggregating data minimizes the number of calls to euwatch-put-data . For example, instead of calling euwatch-put-data multiple times for three data points that are within three seconds of each other, you can aggregate the data into a statistic set that you publish with one call: 



    euwatch-put-data --metric-name PageViewCount --namespace "TestService" -s "Sum=11,Minimum=2,Maximum=5,SampleCount=3" --timestamp 2011-03-14T12:00:00.000


## Publish the value zero
When your data is more sporadic and you have periods that have no associated data, you can choose to publish the value zero (0) for that period or no value at all. You might want to publish zero instead of no value if you use periodic calls to PutMetricData to monitor the health of your application. For example, you can set an Amazon CloudWatch alarm to notify you if your application fails to publish metrics every five minutes. You want such an application to publish zeros for periods with no associated data. 

You might also publish zeros if you want to track the total number of data points or if you want statistics such as minimum and average to include data points with the value 0. 
