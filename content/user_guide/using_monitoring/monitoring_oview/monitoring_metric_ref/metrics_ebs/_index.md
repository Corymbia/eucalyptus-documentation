+++
title = "EBS Metrics and Dimensions"
weight = 30
+++

This section describes the Elastic Block Store (EBS) metrics and dimensions available to CloudWatch.
## Available Metrics for EBS


| Metric | Description | Unit | 
|  :---- |  :---- |  :---- | 
| VolumeReadBytes | The total number of bytes transferred in the period. | Bytes | 
| VolumeWriteBytes | The total number of bytes transferred in the period. | Bytes | 
| VolumeReadOps | The total number of operations in the period. | Count | 
| VolumeWriteOps | The total number of operations in the period. | Count | 
| VolumeTotalReadTime | The total number of seconds spent by all operations that completed in the period. If multiple requests are submitted at the same time, this total could be greater than the length of the period. For example, say the period is 5 minutes (300 seconds); if 700 operations completed during that period, and each operation took 1 second, the value would be 700 seconds. | Seconds | 
| VolumeTotalWriteTime | The total number of seconds spent by all operations that completed in the period. If multiple requests are submitted at the same time, this total could be greater than the length of the period. For example, say the period is 5 minutes (300 seconds); if 700 operations completed during that period, and each operation took 1 second, the value would be 700 seconds. | Seconds | 
| VolumeIdleTime | The total number of seconds in the period when no read or write operations were submitted. | Seconds | 
| VolumeQueueLength | The number of read and write operation requests waiting to be completed in the period. | Count | 


## Available Dimensions for EBS
The only dimension that EBS sends to CloudWatch is the Volume ID. This means that all available statistics are filtered by Volume ID. 

