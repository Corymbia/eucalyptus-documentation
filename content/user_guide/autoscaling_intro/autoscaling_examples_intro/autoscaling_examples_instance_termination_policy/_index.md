+++
title = "Configuring an Instance Termination Policy"
weight = 40
+++

You can control how Auto Scaling determines which instances to terminate. You can specify a termination policy when you create an Auto Scaling group, and you can change the termination policy at any time using the command.You can override the default instance termination policy for your Auto Scaling group with one of the following options: 



| Option | Description | 
|  :---- |  :---- | 
| OldestInstance | The oldest instance in the Auto Scaling group should be terminated. | 
| NewestInstance | The newest instance in the Auto Scaling group should be terminated. | 
| OldestLaunchConfiguration | The first instance created using the oldest launch configuration should be terminated. | 
| Default | Use the default instance termination policy. | 



To configure an instance termination policy: 

Specify the --termination-policies parameter when creating or updating the Auto Scaling group. For example: 

    euscale-update-auto-scaling-group MyScalingGroup --termination-policies "NewestInstance"

Verify that your Auto Scaling group has updated the termination policy by running the following command: `euscale-describe-auto-scaling-groups MyScalingGroup` This command should return output similar to the following: 



    AUTO-SCALING-GROUP	MyScalingGroup	MyLaunchConfig	PARTI00		2	5	2	NewestInstance
    INSTANCE	i-1B853EC3	PARTI00	InService	Healthy	MyLaunchConfig
    INSTANCE	i-ABC53ED7	PARTI00	InService	Healthy	MyLaunchConfig

