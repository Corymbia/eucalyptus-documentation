+++
title = "Route Tables"
weight = 10
+++

A route table defines how traffic is directed in your network. Each subnet in your network has to be associated with one (and only one) route table, but a route table can have multiple subnets associated with it. A default route table (which simply contains a local route that allows communication within the VPC) is automatically created for you when you create your VPC. New subnets will get this route table by default, but you can replace it with a custom route table that enables you to explicitly control subnet traffic. 


{{% notice note %}}
For more information on route tables, see the on Wikipedia. 
{{% /notice %}}
