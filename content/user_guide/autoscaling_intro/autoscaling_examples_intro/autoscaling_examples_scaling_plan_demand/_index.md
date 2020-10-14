+++
title = "Configuring a Demand-Based Scaling Policy"
weight = 20
+++

An Auto Scaling group needs a scaling policy to determine when to perform scaling activities. Auto scaling policies work with CloudWatch to identify metrics and set alarms, which are triggered when the metrics fall outside of a specified value range. To configure a scale-based policy, you need to create the policy, and then create CloudWatch alarms to associate with the policy.In the following example, we will create a demand-based scaling policy. 
{{% notice note %}}
For more information on CloudWatch, go to . 
{{% /notice %}}

## Create Auto Scaling Policies
To create the scaling policies: 

Create a scale-out policy using the following command: 

    euscale-put-scaling-policy MyScaleoutPolicy --auto-scaling-group MyScalingGroup --adjustment=30 --type PercentChangeInCapacity

This command will return a unique Amazon Resource Name (ARN) for the new policy. 
{{% notice note %}}
You will need this ARN to create the Cloudwatch alarms in subsequent steps. 
{{% /notice %}}

{{% notice note %}}
The following example has been split into two lines for legibility. 
{{% /notice %}}


    arn:aws:autoscaling::706221218191:scalingPolicy:5d02981b-f440-4c8f-98f2-8a620dc2b787:
        autoScalingGroupName/MyScalingGroup:policyName/MyScaleoutPolicy

Create a scale-in policy using the following command: 

    euscale-put-scaling-policy MyScaleinPolicy -g MyScalingGroup --adjustment=-2  --type ChangeInCapacity

This command will return output containing a unique Amazon Resource Name (ARN) for the new policy, similar to the following: 
{{% notice note %}}
You will need this ARN to create the Cloudwatch alarms in subsequent steps. 
{{% /notice %}}

{{% notice note %}}
The following example has been split into two lines for legibility. 
{{% /notice %}}


    arn:aws:autoscaling::706221218191:scalingPolicy:d28c6ffc-e9f1-4a48-a79c-8b431794c367:
        autoScalingGroupName/MyScalingGroup:policyName/MyScaleinPolicy


## Create CloudWatch Alarms
To create CloudWatch alarms: 

Create a Cloudwatch alarm for scaling out when the average CPU usage exceeds 80 percent: 
{{% notice note %}}
The following example has been split into multiple lines for legibility. 
{{% /notice %}}


    euwatch-put-metric-alarm AddCapacity  --metric-name CPUUtilization --unit Percent
    --namespace "AWS/EC2" --statistic Average --period 120 --threshold 80 --comparison-operator 
    GreaterThanOrEqualToThreshold --dimensions "AutoScalingGroupName=MyScalingGroup" 
    --evaluation-periods 2 --alarm-actions 
    arn:aws:autoscaling::706221218191:scalingPolicy:5d02981b-f440-4c8f-98f2-8a620dc2b787:
       autoScalingGroupName/MyScalingGroup:policyName/MyScaleoutPolicy

Create a Cloudwatch alarm for scaling in when the average CPU usage falls below 40 percent: 
{{% notice note %}}
The following example has been split into multiple lines for legibility. 
{{% /notice %}}


    euwatch-put-metric-alarm RemoveCapacity --metric-name CPUUtilization --unit Percent
    --namespace "AWS/EC2" --statistic Average  --period 120  --threshold 40  --comparison-operator 
    LessThanOrEqualToThreshold  --dimensions "AutoScalingGroupName=MyScalingGroup" --evaluation-periods 2 
    --alarm-actions 
     arn:aws:autoscaling::706221218191:scalingPolicy:d28c6ffc-e9f1-4a48-a79c-8b431794c367:
      autoScalingGroupName/MyScalingGroup:policyName/MyScaleinPolicy


## Verify Your Alarms and Policies
Once you've created your Auto Scaling policies and CloudWatch alarms, you should verify them.To verify your alarms and policies: 

Use the CloudWatch command `euwatch-describe-alarms` to see a list of the alarms you've created: 

    euwatch-describe-alarms 

This will return output similar to the following: 



    AddCapacity	INSUFFICIENT_DATA	arn:aws:autoscaling::706221218191:scalingPolicy:5d02981b-f440-4c8f-98f2-8a620dc2b787:
       autoScalingGroupName/MyScalingGroup:policyName/MyScaleoutPolicy	
       AWS/EC2	CPUUtilization	120	Average	2	GreaterThanOrEqualToThreshold	80.0
    RemoveCapacity	INSUFFICIENT_DATA	arn:aws:autoscaling::706221218191:scalingPolicy:d28c6ffc-e9f1-4a48-a79c-8b431794c367:
    autoScalingGroupName/MyScalingGroup:policyName/MyScaleinPolicy	
       AWS/EC2	CPUUtilization	120	Average	2	LessThanOrEqualToThreshold	40.0

Use the euscale-describe-policies command to see the scaling policies you've created: 

    euscale-describe-policies --auto-scaling-group MyScalingGroup

This will return output similar to the following (note that this output has been split into multiple lines for legibility): 



    SCALING-POLICY	MyScalingGroup	MyScaleinPolicy	-2	ChangeInCapacity	arn:aws:autoscaling::706221218191:
      scalingPolicy:d28c6ffc-e9f1-4a48-a79c-8b431794c367:
      autoScalingGroupName/MyScalingGroup:policyName/MyScaleinPolicy
    SCALING-POLICY	MyScalingGroup	MyScaleoutPolicy	30	PercentChangeInCapacity	arn:aws:autoscaling::706221218191:
      scalingPolicy:5d02981b-f440-4c8f-98f2-8a620dc2b787:
      autoScalingGroupName/MyScalingGroup:policyName/MyScaleoutPolicy

