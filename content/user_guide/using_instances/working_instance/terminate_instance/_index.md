+++
title = "Terminate an Instance"
weight = 10
+++

The `euca-terminate-instances` command lets you cancel running VM instances. When you terminate instances, you must specify the ID string of the instance(s) you wish to terminate. You can obtain the ID strings of your instances using the euca-describe-instances command. 


{{% notice warning %}}
Terminating an instance can cause the instance and all items associated with the instance (data, packages installed, etc.) to be lost. Be sure to save any important work or data to Walrus or EBS before terminating an instance. 
{{% /notice %}}
To terminate VM instances: 

Enter `euca-describe` instances to obtain the ID of the instances you wish to terminate. Note that an instance ID strings begin with the prefix `i-` followed by an 8-character string: 

    euca-describe-instances
    RESERVATION	r-338206B5	alice	default
    INSTANCE	i-4DCF092C  emi-EC1410C1	192.168.7.24	10.17.0.130 ↵
    running 	mykey 	0 	m1.small 	2010-03-15T21:57:45.134Z ↵
    wind 	eki-822C1344 	eri-BFA91429

Enter `euca-terminate-instances` and the ID string(s) of the instance(s) you wish to terminate: 

    euca-terminate-instances i-4DCF092C
     INSTANCE	i-3ED007C8

