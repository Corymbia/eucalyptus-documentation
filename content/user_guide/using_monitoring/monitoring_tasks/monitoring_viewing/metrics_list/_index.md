+++
title = "List Available Metrics"
weight = 10
+++

You can list available metrics via Euca2ools.**To list available metrics:** 

Enter the following command. 

    euwatch-list-metrics

Eucalyptus returns a listing of all metrics, as shown in the following partial example output: 

    Metric Name         Namespace  Dimensions
    CPUUtilization      AWS/EC2    {InstanceId=i-5431413d}
    CPUUtilization      AWS/EC2    {InstanceType=m1.medium}
    DiskReadBytes       AWS/EC2    {InstanceId=i-1d3d4d74}
    DiskReadBytes       AWS/EC2    {InstanceType=m1.medium}
    DiskReadOps         AWS/EC2    {InstanceId=i-d3c8baba}
    DiskReadOps         AWS/EC2    {InstanceType=m1.medium}
    DiskWriteBytes      AWS/EC2    {InstanceId=i-6732420e}	
    DiskWriteBytes      AWS/EC2    {InstanceType=m1.medium}
    DiskWriteOps        AWS/EC2    {InstanceId=i-e03d4d89}
    DiskWriteOps        AWS/EC2    {InstanceType=m1.medium}
    NetworkIn           AWS/EC2    {InstanceId=i-e0304089}
    NetworkIn           AWS/EC2    {InstanceType=m1.medium}
    NetworkOut          AWS/EC2    {InstanceId=i-69334300}
    NetworkOut          AWS/EC2    {InstanceType=m1.medium}
    StatusCheckFailed		 AWS/EC2 {InstanceId=i-6f8418e6}
    StatusCheckFailed      	  AWS/EC2 {InstanceType=m1.medium}
    StatusCheckFailed_Instance      AWS/EC2 {InstanceId=i-6f8418e6}
    StatusCheckFailed_Instance      AWS/EC2 {InstanceType=m1.medium}
    StatusCheckFailed_System        AWS/EC2 {InstanceId=i-6f8418e6}
    StatusCheckFailed_System        AWS/EC2 {InstanceType=m1.medium}

