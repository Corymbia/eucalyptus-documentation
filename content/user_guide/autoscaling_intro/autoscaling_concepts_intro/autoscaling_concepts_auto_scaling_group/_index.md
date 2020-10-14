+++
title = "Understanding Auto Scaling Groups"
weight = 20
+++

An Auto Scaling group is the central component of Auto Scaling. An Auto Scaling group defines the parameters for the Eucalyptus instances are used for scaling, as well as the minimum, maximum, and (optionally) the desired number of instances to use for Auto Scaling your application. If you don't specify the desired number of instances in your Auto Scaling group, the default value will be the same as the minimum number of instances defined. 

In addition to instance and capacity definitions, each Auto Scaling group must specify one (and only one) launch configuration. 

For more information, see [Creating a Basic Auto Scaling Configuration]({{< ref autoscaling_examples_basic_config.md >}}) . 

