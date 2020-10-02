+++
title = "CloudWatch Concepts"
weight = 5
+++

This section describes the terminology and concepts you need in order to understand and use CloudWatch.
## Metric
A metric is a time-ordered set of data points. You can get metric data from Eucalyptus cloud resources (like instances or volumes), or you can publish your own set of custom metric data points to CloudWatch. You then retrieve statistics about those data points as an ordered set of time-series data. 

Data points represent values of a variable over time. For example you can get metrics for the CPU usage of a particular instance, or for the latency of an elastic load balancer (ELB). 

Each metric is uniquely defined by a name, a namespace, and zero or more dimensions. Each data point has a time stamp, and (optionally) a unit of measure. When you request statistics, the returned data stream is identified by namespace, metric name, dimension, and (optionally) the unit. For more information about Eucalyptus-supported metrics, see [](monitoring_metric_ref.dita) . 

CloudWatch stores your metric data for two weeks. You can publish metric data from multiple sources, such as incoming network traffic from dozens of different instances, or requested page views from several different web applications. You can request statistics on metric data points that occur within a specified time window. 


## Namespace
A namespace is a conceptual container for a collection of metrics. Eucalyptus treats metrics in different namespaces as unique. This means that metrics from different services cannot mistakenly be aggregated into the same statistical set. 

Namespace names are strings you define when you create a metric. The names must be valid XML characters, typically containing the alphanumeric characters "0-9A-Za-z" plus "."(period), "-" (hyphen), "_" (underscore), "/" (slash), "#" (hash), and ":" (colon). All Eucalyptus services that provide CloudWatch data follow the convention AWS/<service>, such as AWS/EC2 and AWS/ELB. For more information, see [](monitoring_namespaces.dita) . 


{{% notice note %}}
A namespace name must be less than 256 characters. There is no default namespace. You must specify a namespace for each data element you put into CloudWatch. 
{{% /notice %}}

## Dimension
A dimension is a name-value pair that uniquely identifies a metric. A dimension helps you design a conceptual structure for your statistics plan. Because dimensions are part of the unique identifier for a metric, metric name, namespace, and dimension key-value pairs define unique metrics. 

You specify dimensions when you create a metric with the euwatch-put-data command. Eucalyptus services that report data to CloudWatch also attach dimensions to each metric. You can use dimensions to filter result sets that CloudWatch queries return. For example, you can get statistics for a specific instance by calling euwatch-get-stats with the InstanceID dimension set to a specific instance ID. 

For Eucalyptus metrics, CloudWatch can aggregate data across select dimensions. For example, if you request a metric in the AWS/EC2 namespace and do not specify any dimensions, CloudWatch aggregates all data for the specified metric to create the statistic that you requested. However, CloudWatch does not aggregate across dimensions for custom metrics 


{{% notice note %}}
You can assign up to ten dimensions to a metric. 
{{% /notice %}}

## Time Stamp
Each metric data point must be marked with a time stamp. The time stamp can be up to two weeks in the past and up to two hours into the future. If you do not provide a time stamp, CloudWatch creates a time stamp for you based on the time the data element was received. 

The time stamp you use in the request must be a dateTime object, with the complete date plus hours, minutes, and seconds. For example: 2007-01-31T23:59:59Z. For more information, go to [http://www.w3.org/TR/xmlschema-2/#dateTime](http://www.w3.org/TR/xmlschema-2/#dateTime) . Although it is not required, we recommend you provide the time stamp in the Coordinated Universal Time (UTC or Greenwich Mean Time) time zone. When you retrieve your statistics from CloudWatch, all times reflect the UTC time zone. 


## Unit
A unit represents a statistic's measurement in time or amount. For example, the units for the instance NetworkIn metric is Bytes because NetworkIn tracks the number of bytes that an instance receives on all network interfaces. 

You can also specify a unit when you create a custom metric. Units help provide conceptual meaning to your data. Metric data points you create that specify a unit of measure, such as Percent, will be aggregated separately. The following list provides some of the more common units that CloudWatch supports: 



* Seconds 
* Bytes 
* Bits 
* Percent 
* Count 
* Bytes/Second (bytes per second) 
* Bits/Second (bits per second) 
* Count/Second (counts per second) 
* None (default when no unit is specified) 
Though CloudWatch attaches no significance to a unit, other applications can derive semantic information based on the unit you choose. When you publish data without specifying a unit, CloudWatch associates it with the None unit. When you get statistics without specifying a unit, CloudWatch aggregates all data points of the same unit together. If you have two otherwise identical metrics with different units, two separate data streams will be returned, one for each unit. 


## Statistic
A statistic is computed aggregation of metric data over a specified period of time. CloudWatch provides statistics based on the metric data points you or Eucalyptus provide. Aggregations are made using the namespace, metric name, dimensions, and the data point unit of measure, within the time period you specify. The following table describes the available statistics. 


| Statistic | Description | 
|  :---- |  :---- | 
| Minimum | The lowest value observed during the specified period. You can use this value to determine low volumes of activity for your application. | 
| Maximum | The highest value observed during the specified period. You can use this value to determine high volumes of activity for your application. | 
| Sum | All values submitted for the matching metric added together. You can use this statistic for determining the total volume of a metric. | 
| Average | The value of Sum / SampleCount during the specified period. By comparing this statistic with the Minimum and Maximum, you can determine the full scope of a metric and how close the average use is to the Minimum and Maximum. This comparison helps you to know when to increase or decrease your resources as needed. | 
| SampleCount | The count (number) of data points used for the statistical calculation. | 


## Period
A period is the length of time, in seconds, associated with a specific CloudWatch statistic. Each statistic represents an aggregation of the metrics data collected for a specified period of time. You can adjust how the data is aggregated by varying the length of the period. A period can be as short as one minute (60 seconds) or as long as two weeks (1,209,600 seconds). 

The values you select for the StartTime and EndTime options determine how many periods CloudWatch returns. For example, if you set values for the Period, EndTime, and StartTime options for 60 seconds, CloudWatch returns an aggregated set of statistics for each minute of the previous hour. If you want statistics aggregated into ten-minute blocks, set Period to 600. For statistics aggregated over the entire hour, use a Period value of 3600. 

Periods are also an important part of the CloudWatch alarms feature. When you create an alarm to monitor a specific metric, you are asking CloudWatch to compare that metric to the threshold value that you supplied. You have control over how CloudWatch makes that comparison. You can specify the period over which the comparison is made, as well as how many consecutive periods the threshold must be breached before you are notified. 


## Aggregation
CloudWatch aggregates statistics according a length of time that you set. You can publish as many data points as you want with the same or similar time stamps. CloudWatch aggregates these data points by period length. You can publish data points for a metric that share not only the same time stamp, but also the same namespace and dimensions. 

Subsequent calls to euwatch-get-stats return aggregated statistics about those data points. You can even do this in one euwatch-put-data request. CloudWatch accepts multiple data points in the same euwatch-put-data call with the same time stamp. You can also publish multiple data points for the same or different metrics, with any time stamp. The size of a euwatch-put-data request, however, is limited to 8KB for HTTP GET requests and 40KB for HTTP POST requests. You can include a maximum of 20 data points in one PutMetricData request. 

For large data sets that would make the use of euwatch-put-data impractical, CloudWatch allows you to insert a pre-aggregated data set called a StatisticSet. With StatisticSets you give CloudWatch the Min, Max, Sum, and SampleCount of a number of data points. A common use case for StatisticSets is when you are collecting data many times in a minute. For example, if you have a metric for the request latency of a server, it doesn’t make sense to do a euwatch-put-data request with every request. We suggest you collect the latency of all hits to that server, aggregate them together once a minute and send that StatisticSet to CloudWatch. 

CloudWatch doesn't differentiate the source of a metric. If you publish a metric with the same namespace and dimensions from different sources, CloudWatch treats this as a single metric. This can be useful for service metrics in a distributed, scaled system. For example, all the hosts in a web server application could publish identical metrics representing the latency of requests they are processing. CloudWatch treats these as a single metric, allowing you to get the statistics for minimum, maximum, average, and sum of all requests across your application. 


## Alarm
An alarm watches a single metric over a time period you set, and performs one or more actions based on the value of the metric relative to a given threshold over a number of time periods. CloudWatch alarms will not invoke actions just because they are in a particular state. The state must have changed and been maintained for a specified number of periods. 

For example, [Auto Scaling](autoscaling_intro.dita) works with CloudWatch alarms to perform scaling activities. When an Auto Scaling activity reacts to a CloudWatch alarm, the cooldown period is the amount of time after the activity takes place where further Auto Scaling activity is suspended. This is to allow time for the Auto Scaling activities (such as new instance launches or terminations) to fully complete so that resources are not unnecessarily launched or terminated. You can specify this amount of time; if you don't specify a cooldown period, Auto Scaling uses a default cooldown period of 300 seconds (5 minutes). 

After an alarm invokes an action due to a change in state, the alarm continues to invoke the action for every period that the alarm remains in the new state. 

An alarm has three possible states: 



* : The metric is within the defined threshold. 
* : The metric is outside of the defined threshold. 
* : The alarm has just started, the metric is not available, or not enough data is available for the metric to determine the alarm state. 
The following lists some common features of alarms: 



* You can create up to 5000 alarms per Eucalyptus account. To create or update an alarm, use the command. 
* You can list any or all of the currently configured alarms, and list any alarms in a particular state using the command. 
* You can disable and enable alarms by using the and commands 
* You can test an alarm by setting it to any state using the command. This temporary state change lasts only until the next alarm comparison occurs. 
* Finally, you can view an alarm's history using the command. CloudWatch preserves alarm history for two weeks. Each state transition is marked with a unique time stamp. In rare cases, your history might show more than one notification for a state change. The time stamp enables you to confirm unique state changes. 
