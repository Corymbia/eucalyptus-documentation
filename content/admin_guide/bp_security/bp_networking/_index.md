+++
title = "Networking Modes"
weight = 10
+++

This topic describes the recommendations for networking modes.A Eucalyptus deployment can be configured in EDGE (AWS EC2 Classic compatible) or VPCMIDO (AWS VPC compatible) networking modes. In both modes, by default, instances are not allowed to send traffic with spoofed IP and/or MAC addresses and receive traffic that are not destined to their own IP and/or MAC addresses. Security groups should be used to control the ingress traffic to instances (EDGE and VPCMIDO modes) and to control the egress traffic from instances (VPCMIDO mode). 

VPCMIDO mode offers many security features not present in EDGE mode. Instances of different accounts are deployed in user-defined isolated networks within a Eucalyptus cloud. A combination of security features including VPC, VPC subnets, security groups, source/destination check configuration, route tables, internet gateways, and NAT gateways can be used to selectively enable and configure network access to/from instances or group of instances. 

For more information about choosing a networking modes, see [Plan Networking Modes]({{< ref planning_networking_modes.md >}}) . 

