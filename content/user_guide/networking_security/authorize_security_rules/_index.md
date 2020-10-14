+++
title = "Authorize Security Group Rules"
weight = 50
+++

By default, a security group prevents incoming network traffic from all sources. You can modify network rules and allow incoming traffic to security groups from specified sources using the euca-authorize command. 

To authorize security group rules: 

Use `euca-authorize` to authorize port 22 access to your default group. Enter the following command: 

    euca-authorize -P <protocol> -p <port_number> \
    -s <CIDR_source_network> <group_name>

The following example allows all incoming SSH traffic on port 22 to access to the security group `mygroup` . The CIDR source network, `0.0.0.0/0` , refers to any source. 

    euca-authorize -P tcp -p 22 -s 0.0.0.0/0 mygroup 
     GROUP	mygroup ↵
     PERMISSION	mygroup	ALLOWS	tcp	22	22	FROM	CIDR

Instead of specifying a CIDR source, you can specify another security group. The following example allows access to the security group `mygroup` from the `someothergroup` security group using SSH on port 22. 

    euca-authorize --source-group someothergroup \
    --source-group-user someotheruser -P tcp -p 22 mygroup

