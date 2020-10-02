+++
title = "Get Statistics for a Metric"
weight = 10
+++

You can get statistics for metrics via Euca2ools.**To get statistics for a metric:** 

Enter the following command. 
     euwatch-get-stats -n NAMESPACE -s STAT1,STAT2,...
                			[--dimensions KEY1=VALUE1,KEY2=VALUE2,...]
                			[--start-time YYYY-MM-DDThh:mm:ssZ]
                			[--end-time YYYY-MM-DDThh:mm:ssZ] [--period SECONDS]
                			[--unit UNIT] [--show-empty-fields] [-U URL]
                			[--region USER@REGION] [-I KEY_ID] [-S KEY]
                			[--security-token TOKEN] [--debug] [--debugger]
                			[--version] [-h]
                			METRIC

The following example returns the average CPU utilization for the i-c08804a9 instance at one hour resolution. 


    euwatch-get-stats --namespace "AWS/EC2" --statistics "Average" \
    --dimensions "InstanceId=i-c08804a9" --start-time 2016-12-14T23:00:00.000Z \
    --end-time 2016-12-15T23:00:00.000Z --period 3600  CPUUtilization

The following example returns CPU utilization for all of your cloud's instances. 


    euwatch-get-stats --namespace "AWS/EC2" --statistics "Average,Minimum,Maximum" \
    --start-time 2016-02-14T23:00:00.000Z --end-time 2016-03-14T23:00:00.000Z \
    --period 3600 CPUUtilization

