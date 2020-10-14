+++
title = "Elastic Network Interfaces (ENIs)"
weight = 20
+++

In Eucalyptus VPC, networking to instances (VMs) is delivered in the form of Elastic Network Interfaces (ENIs). ENIs are virtual network interfaces that can be attached to and/or detached from instances in a VPC. 

Attributes of an ENI (private address, public address, Elastic IP, MAC address, security groups, and source/destination check flag) follow the ENI as it is detached from an instance and attached to another instance. An instance in a VPC has a default ENI attached, which is called the primary ENI. The Primary ENI cannot be detached. 

Additional ENIs (up to a total of eight) can be attached to instances as needed. ENIs in different subnets can be attached to the same instance, but all ENIs and the instance must reside in the same Availability Zone. Users may need to manually bring up and configure secondary ENIs from within instances. 

