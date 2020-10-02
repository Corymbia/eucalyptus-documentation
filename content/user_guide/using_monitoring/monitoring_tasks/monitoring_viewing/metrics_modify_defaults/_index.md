+++
title = "Modify Metric Polling Timing"
weight = 10
+++

You can modify metrics timing and reporting defaults.When using the default CloudWatch properties, metrics reporting can take around 15 minutes: 

1. 5 minutes to receive a sensor data point for an instance. 
1. 5 more minutes to receive a second sensor data point for an instance. 
1. 1 more minute to calculate the difference between these two and send a single data point to CloudWatch. 
1. 1 more minute for CloudWatch to put the data in the database, making it available for a call. 
1. 5 more minutes for info to be available in the database. 

{{% notice note %}}
The above workflow is sequential and cumulative. 
{{% /notice %}}


The sensor data point timing values can be shortened by changing variables in the CLC. 


{{% notice note %}}
These changes will increase network traffic as polling will be done more frequently. 
{{% /notice %}}
**To modify metrics defaults:** 

Modify the default polling interval CLC variable to a number less than 5. 
    cloud.monitor.default_poll_interval_mins

This is how often the CLC sends a request to the CC for sensor data. Default value is 5 minutes. Modify the history size CLC variable to a number less than 5. 
    cloud.monitor.history_size

This is how many data value samples are sent in each sensor data request. The default value is 5. The frequency requests is either 1 minute (if the `cloud.monitor.default_poll_interval_mins` is 1 minute) or half the value of `cloud.monitor.default_poll_interval_mins` if that value is greater). So by default, with a `cloud.monitor.default_poll_interval_mins` of 5 minutes and `cloud.monitor.history_size` size of 5, every 5 minutes the CLC asks for the last 5 data points from the CC, which should be timed for every 2.5 minutes (e.g., 2.5 minutes ago, 5 minutes ago, 7.5 minutes ago, and 10 minutes ago). 
{{% notice note %}}
These values may be skewed a bit based on the time the CC uses. 
{{% /notice %}}
For more information, see [](../euca2ools-guide/euca-properties.dita#eucaproperties) . 

