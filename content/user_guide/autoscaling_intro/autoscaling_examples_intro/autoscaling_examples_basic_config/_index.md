+++
title = "Creating a Basic Auto Scaling Configuration"
weight = 10
+++

Auto scaling requires two basic elements to function properly: a launch configuration and an Auto Scaling group. The following examples show how to set up the basic elements of an Auto Scaling configuration.
## Create a Launch Configuration
The launch configuration specifies the parameters that Auto Scaling will use when launching new instances for your Auto Scaling group. In this example, we will create a launch configuration with the minimum required parameters - in this case, we set up a launch configuration that specifies that all instances launched in the Auto Scaling group will be of instance type and use the image.To create a launch configuration: 

Enter the following command: `euscale-create-launch-config MyLaunchConfig --image-id emi-00123456 --instance-type m1.small` To verify the launch configuration, enter the following command: `euscale-describe-launch-configs MyLaunchConfig` You should see output similar to the following: 



    LAUNCH-CONFIG	MyLaunchConfig	emi-00123456	m1.small

You've now created a launch configuration.. 
## Create an Auto Scaling Group
The Auto Scaling group contains settings like the minimum, maximum, and desired number of Eucalyptus instances. At minimum, you must specify the name of the Auto Scaling group, the name of an existing launch configuration, the availability zone, and the minimum and maximum number of instances that should be running. In the following example, we will create an Auto Scaling group called MyScalingGroup in availability zone PARTI00, with a minimum size of 2 and a maximum size of 5.To create an Auto Scaling group: Enter the following command: 

    euscale-create-auto-scaling-group MyScalingGroup --launch-configuration
                        		MyLaunchConfig --availability-zones PARTI00 --min-size 2 --max-size 5
                        		--desired-capacity 2

Enter the following command to verify the Auto Scaling group you just created: 

    euscale-describe-auto-scaling-groups MyScalingGroup

This command will return output similar to the following: 



    AUTO-SCALING-GROUP	MyScalingGroup	MyLaunchConfig	PARTI00		2	5	2	Default
    INSTANCE	i-1B853EC3	PARTI00	InService	Healthy	MyLaunchConfig
    INSTANCE	i-ABC53ED7	PARTI00	InService	Healthy	MyLaunchConfig

Once you've created the Auto Scaling group, Auto Scaling will launch the appropriate number of instances. 