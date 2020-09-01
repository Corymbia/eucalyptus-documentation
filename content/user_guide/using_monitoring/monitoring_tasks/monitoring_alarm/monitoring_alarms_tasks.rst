+++
title = "Create an Alarm"
weight = 5
+++

..  _monitoring_alarms_tasks:

You can create a CloudWatch alarm using a resource's metric, and then add an action using the action’s dedicated Amazon Resource Name (ARN). You can add the action to any alarm state. {{% notice note %}}Eucalyptus currently only supports actions for executing Auto Scaling policies. {{% /notice %}}To create an alarm, perform the following step. 

Enter the following command: 

.. code::

  euwatch-put-metric-alarm [alarm_name] --unit Percent --namespace "AWS/EC2" 
  -- dimensions "InstanceId=[instance_id]" --statistic [statistic] --metric-name	
  [metric] --comparison-operator [operator] --threshold [value] --period	
  [seconds] --evaluation-periods [value] -- alarm-actions [action]

For example, the following triggers an Auto Scaling policy if the average CPUUtilization is less than 10 percent over a 24 hour period. 

.. code::

  euwatch-put-metric-alarm test-Alarm --unit Percent --namespace "AWS/EC2" 
  -- dimensions "InstanceId=i-abc123" --statistic Average --metric-name CPUUtilization 
  --comparison-operator LessThanThreshold --threshold 10 --period 86400 
  --evaluation-periods 4 -- alarm-actions arn:aws:autoscaling::429942273585:scalingPolicy:
  12ad560b-58b2-4051-a6d3-80e53b674de4:autoScalingGroupName/testgroup01:
  policyName/testgroup01-pol01

