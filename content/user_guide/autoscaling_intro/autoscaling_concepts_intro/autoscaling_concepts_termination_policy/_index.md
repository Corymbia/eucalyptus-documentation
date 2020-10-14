+++
title = "Understanding Instance Termination Policies"
weight = 50
+++

Before Auto Scaling selects an instance to terminate, it first identifies the availability zone used by the group that contains the most instances. If all availability zones have the same number of instances, Auto Scaling selects a random availability zone, and then uses the termination policy to select the instance within that randomly selected availability zone for termination. 

By default, Auto Scaling chooses the instance that was launched with the oldest launch configuration. If more than one instance was launched using the oldest launch configuration, Auto Scaling the instance that was created first using the oldest launch configuration. 

You can override the default instance termination policy for your Auto Scaling group with one of the following options: 



| Option | Description | 
|  :---- |  :---- | 
| OldestInstance | The oldest instance in the Auto Scaling group should be terminated. | 
| NewestInstance | The newest instance in the Auto Scaling group should be terminated. | 
| OldestLaunchConfiguration | The first instance created using the oldest launch configuration should be terminated. | 
| Default | Use the default instance termination policy. | 



You can have more than one termination policy per Auto Scaling group. The termination policies are executed in the order they were created. 

For more information, go to [Configuring an Instance Termination Policy]({{< ref autoscaling_examples_instance_termination_policy.md >}}) . 

