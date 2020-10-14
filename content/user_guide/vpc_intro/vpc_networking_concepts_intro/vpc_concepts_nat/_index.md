+++
title = "Network Address Translation (NAT) Gateways"
weight = 50
+++

NAT Gateways enable instances in private VPC subnets to initiate communication with the Internet (and receive responses), but prevents connections to be initiated from the Internet. Traffic bound to the Internet from instances in private subnets should be directed to a NAT gateway (through the use of route tables), which will translate the source address to its own Elastic IP and route it to the Internet. The destination will send a response back to the Elastic IP (i.e., the NAT gateway), where the address translation will be reversed and delivered to the originating private IP. 

NAT Gateways should be created in public VPC subnets, and have an Elastic IP associated. Private VPC subnets should have its route table manually updated to direct Internet-bound traffic to a NAT gateway. 

