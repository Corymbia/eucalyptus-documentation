+++
title = "Understanding Launch Configurations"
weight = 10
+++

The launch configuration defines the settings used by the Eucalyptus instances launched within an Auto Scaling group. This includes the image name, the instance type, key pairs, security groups, and block device mappings. You associate the launch configuration with an Auto Scaling group. Each Auto Scaling group can have one (and only one) associated launch configuration. 

Once you've created a launch configuration, you can't change it; you must create a new launch configuration and then associate it with an Auto Scaling group. After you've created and attached a new launch configuration to an Auto Scaling group, any new instances will be launched using parameters defined in the new launch configuration; existing instances in the Auto Scaling group are not affected. 

For more information, see [Creating a Basic Auto Scaling Configuration]({{< ref autoscaling_examples_basic_config.md >}}) . 

