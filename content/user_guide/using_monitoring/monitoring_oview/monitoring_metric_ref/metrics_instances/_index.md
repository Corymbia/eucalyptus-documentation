+++
title = "Instance Metrics and Dimensions"
weight = 20
+++

This section describes the instance metrics and dimensions available to CloudWatch.
## Available Metrics for Instances


| Metric | Description | Unit | 
|  :---- |  :---- |  :---- | 
| CPUUtilization | The percentage of allocated EC2 compute units that are currently in use on the instance. This metric identifies the processing power required to run an application upon a selected instance. | Percent | 
| DiskReadOps | Completed read operations from all ephemeral disks available to the instance (if your instance uses EBS, see EBS Metrics.) This metric identifies the rate at which an application reads a disk. This can be used to determine the speed in which an application reads data from a hard disk. | Count | 
| DiskWriteOps | Completed write operations to all ephemeral disks available to the instance (if your instance uses Amazon EBS, see Amazon EBS Metrics.) This metric identifies the rate at which an application writes to a hard disk. This can be used to determine the speed in which an application saves data to a hard disk. | Count | 
| DiskReadBytes | Bytes read from all ephemeral disks available to the instance (if your instance uses Amazon EBS, see Amazon EBS Metrics.) This metric is used to determine the volume of the data the application reads from the hard disk of the instance. This can be used to determine the speed of the application. | Bytes | 
| DiskWriteBytes | Bytes written to all ephemeral disks available to the instance (if your instance uses Amazon EBS, see Amazon EBS Metrics.) This metric is used to determine the volume of the data the application writes onto the hard disk of the instance. This can be used to determine the speed of the application. | Bytes | 
| NetworkIn | The number of bytes received on all network interfaces by the instance. This metric identifies the volume of incoming network traffic to an application on a single instance. | Bytes | 
| NetworkOut | The number of bytes sent out on all network interfaces by the instance. This metric identifies the volume of outgoing network traffic to an application on a single instance. | Bytes | 
| StatusCheckFailed | A combination of StatusCheckFailed_Instance and StatusCheckFailed_System that reports if either of the status checks has failed. Values for this metric are either 0 (zero) or 1 (one.) A zero indicates that the status check passed. A one indicates a status check failure. | Count | 
| StatusCheckFailed_Instance | Reports whether the instance has passed the EC2 instance status check in the last 5 minutes. Values for this metric are either 0 (zero) or 1 (one.) A zero indicates that the status check passed. A one indicates a status check failure. | Count | 
| StatusCheckFailed_System | Reports whether the instance has passed the EC2 system status check in the last 5 minutes. Values for this metric are either 0 (zero) or 1 (one.) A zero indicates that the status check passed. A one indicates a status check failure. | Count | 


## Available Dimensions for Instances
You can filter the instance data using any of the dimensions in the following table. 



| Dimension | Description | 
|  :---- |  :---- | 
| AutoScalingGroupName | This dimension filters the data you request for all instances in a specified capacity group. An AutoScalingGroup is a collection of instances you define if you're using the Auto Scaling service. This dimension is available only for instance metrics when the instances are in such an Auto Scaling group. | 
| ImageId | This dimension filters the data you request for all instances running this Eucalyptus Machine Image (EMI). | 
| InstanceId | This dimension filters the data you request for the identified instance only. This helps you pinpoint an exact instance from which to monitor data. | 
| InstanceType | This dimension filters the data you request for all instances running with this specified instance type. This helps you categorize your data by the type of instance running. For example, you might compare data from an m1.small instance and an m1.large instance to determine which has the better business value for your application. | 

