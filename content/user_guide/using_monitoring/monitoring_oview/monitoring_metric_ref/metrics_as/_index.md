+++
title = "Auto Scaling Metrics and Dimensions"
weight = 40
+++

This section discusses the Auto Scaling metrics and dimensions available to CloudWatch. 


## Available Metrics for Auto Scaling


| Metric | Description | Unit | 
|  :---- |  :---- |  :---- | 
| GroupMinSize | The minimum size of the Auto Scaling group. | Count | 
| GroupMaxSize | The maximum size of the Auto Scaling group. | Count | 
| GroupDesiredCapacity | The number of instances that the Auto Scaling group attempts to maintain. | Count | 
| GroupInServiceInstances | The number of instances that are running as part of the Auto Scaling group. This metric does not include instances that are pending or terminating. | Count | 
| GroupPendingInstances | The number of instances that are pending. A pending instance is not yet in service. This metric does not include instances that are in service or terminating. | Count | 
| GroupTerminatingInstances | The number of instances that are in the process of terminating. This metric does not include instances that are in service or pending. | Count | 
| GroupTotalInstances | The total number of instances in the Auto Scaling group. This metric identifies the number of instances that are in service, pending, and terminating. | Count | 


## Available Dimensions for Auto Scaling
The only dimension that Auto Scaling sends to CloudWatch is the name of the Auto Scaling group. This means that all available statistics are filtered by Auto Scaling group name. 

