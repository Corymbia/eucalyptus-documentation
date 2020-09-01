+++
title = "Plan Networking Modes"
weight = 5
chapter = true
+++

..  _planning_networking_modes:



=====================
Plan Networking Modes
=====================

These networking modes are designed to allow you to choose an appropriate level of security and flexibility for your cloud. The purpose is to direct Eucalyptus to use different network features to manage the virtual networks that connect VMs to each other and to clients external to Eucalyptus . 

Eucalyptus networking modes are generally modeled after AWS networking capabilities. In legacy AWS accounts, you have the ability to choose EC2 Classic network mode or VPC network mode. New AWS accounts do not have this flexibility and are forced into using VPC. Eucalyptus VPCMIDO mode is similar to AWS VPC in that it allows users to fully manage their cloud network, including the definition of a Classless Inter-Domain Routing (CIDR) block, subnets, and security groups with rules for additional protocols beyond the default three (UDP, TCP, and ICMP) available in EC2 Classic networking. 

Your choice of networking mode depends on the following considerations: 

* Does your cloud need to mimic behavior in your AWS account? If you need EC2-Classic behavior, select EDGE mode. If you need EC2-VPC behavior, select VPCMIDO mode. 

* Do you need to create security group rules with additional protocols (e.g., all protocols, RDP, XTP, etc.)? If so, choose VPCMIDO mode. 

* If there is no specific requirement for either mode, then VPCMIDO mode is recommended given its flexibility and networking features. 



Each networking mode is described in the following sections. 

