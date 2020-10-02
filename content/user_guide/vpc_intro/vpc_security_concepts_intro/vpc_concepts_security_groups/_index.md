+++
title = "Security Groups"
weight = 10
+++

A security group is a mechanism that allows you to control inbound and outbound traffic for your VPC. A security group has rules that specify what kinds of traffic are allowed in and out of instances (VMs) running in your VPC. 

A VPC comes with a default security group that allows inbound traffic from other instances assigned to the same security group, and allows all outbound traffic. You can change the rules for the default security group, but you can't delete it. 

If you don't specify a security group when you launch an instance in your VPC, the instance will be associated with the default security group. 

