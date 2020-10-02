+++
title = "Plan Your Installation"
weight = 5
chapter = true
+++


## Plan Your Installation
Before you install Eucalyptus components on your machines, we recommend that you take the time to plan how you want to install it.
{{% notice note %}}
If you are upgrading from an existing release, see . 
{{% /notice %}}
To successfully plan for your Eucalyptus installation, you must determine two things: 



* Think about the application workload performance and resource utilization tuning. Think about how many machines you want on your system. 
* Use your existing architecture and policies to determine the networking features you want to enable: EC2 Classic Networking or EC2 VPC Networking. Think about the public network (not necessarily the IPv4 public space, but the network that users will access), delegating IP addresses to , and . 
This section describes how to evaluate each tradeoff to determine the best choice to make, and how to verify that the resource environment can support the features that are enabled as a consequence of making a choice. 

By the end of this section, you should be able to specify how you will deploy Eucalyptus in your environment, any tradeoffs between feature set and flexibility, and where your deployment will integrate with existing infrastructure systems. 

