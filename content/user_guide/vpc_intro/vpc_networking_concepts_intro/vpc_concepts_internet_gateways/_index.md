+++
title = "Internet Gateways"
weight = 40
+++

An Internet gateway is an object that runs inside of your VPC and provides communication between VPC instances and the Internet. 

To use an Internet gateway in your VPC, you attach the gateway to your VPC, make sure your route tables direct Internet traffic to the Internet gateway, and configure your security groups to allow traffic through. 

By default, instances loaded into any non-default VPC have private IP addresses (so they can communicate with other instances in the same VPC), but they do not have public IP addresses. For an instance to be able to communicate with the Internet gateway, it must have an associated public IP address. The default VPC comes with a pre-configured Internet gateway, and all instances that are launched into the default subnet receive a public IP address, so these instances have Internet access. 

