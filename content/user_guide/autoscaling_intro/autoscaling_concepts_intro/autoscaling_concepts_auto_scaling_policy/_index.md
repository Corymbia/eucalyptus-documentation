+++
title = "Understanding Auto Scaling Policies"
weight = 10
+++

An Auto Scaling policy defines how to perform scaling actions in response to CloudWatch alarms. Auto scaling policies can either *scale-in* , which terminates instances in your Auto Scaling group, or *scale-out* , which will launch new instances in your Auto Scaling group. You can define an Auto Scaling policy based on demand, or based on a fixed schedule. 

**Demand-Based Auto Scaling Policies** 

Demand-based Auto Scaling policies scale your application dynamically based on CloudWatch metrics (such as average CPU utilization) gathered from the instances running in your scaling group. For example, you can configure a CloudWatch alarm to monitor the CPU usages of the instances in your Auto Scaling group. A CloudWatch alarm definition includes *thresholds* - minimum and maximum values for the defined metric - that will cause the alarm to fire. 


{{% notice note %}}
For more information on CloudWatch, go to . 
{{% /notice %}}
For example, you can define the lower and upper thresholds of the CloudWatch alarm at 40% and 80% CPU usage. Once you've created the CloudWatch alarm, you can create a scale-out policy that launches 10 new instances when the CloudWatch alarm breaches the upper threshold (the average CPU usage is at or above 80%), and a scale-in policy that terminates 10 instances when the CloudWatch alarm breaches the lower threshold (the average CPU usage of the instances in the Auto Scaling group falls below 40%). Your Auto Scaling group will execute the appropriate Auto Scaling policy when it receives the message from the CloudWatch alarm. 

**Cooldown Period** 

A *cooldown period* is the amount of time after an Auto Scaling activity takes place where further Auto Scaling activity is suspended. This is to allow time for the Auto Scaling activities (such as new instance launches or terminations) to fully complete so that resources are not unnecessarily launched or terminated. You can specify this amount of time; if you don't specify a cooldown period, Auto Scaling uses a default cooldown period of 300 seconds (5 minutes). 

For more information, go to [Configuring a Demand-Based Scaling Policy](autoscaling_examples_scaling_plan_demand.dita) . 

