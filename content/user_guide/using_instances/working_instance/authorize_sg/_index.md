+++
title = "Authorize Security Groups"
weight = 10
+++

Before you can log in to an instance, you must authorize access to that instance. This done by configuring a security group for that instance. 

A security group is a set of networking rules applied to instances associated with a group. When you first create an instance, it is assigned to a default security group that denies incoming network traffic from all sources. To allow login and usage of a new instance, you must authorize network access to the default security group with the euca-authorize command. 

To authorize a security group, use euca-authorize with the name of the security group, and the options of the network rules you want to apply. 

    euca-authorize <security_group>

Use the following command to grant unlimited network access using SSH (TCP, port 22) and VNC (TCP, ports 5900 to 5910) to the security group `default` : 

    euca-authorize -P tcp -p 22 -s 0.0.0.0/0 default
    euca-authorize -P tcp -p 5900-5910 -s 0.0.0.0/0 default


