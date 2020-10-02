+++
title = "Default VPCs"
weight = 10
+++

Starting with Eucalyptus versions 4.1 and later, when you create an account in your Eucalyptus cloud in VPCMIDO network mode, you get a default VPC with a single public subnet and an attached Internet gateway. All instances that are created in this account that do not explicitly specify a VPC are placed into this default VPC and given a public IP address and behave like 'classic' AWS EC2 instances. 

