+++
title = "Subnets and IP Addressing"
weight = 20
+++

A virtual private cloud (VPC) is a virtual network that is logically isolated from other virtual networks in your Eucalyptus cloud. 


{{% notice note %}}
For more information about CIDR notation, see the on Wikipedia. 
{{% /notice %}}
**Private IP Addresses** 

When you create a VPC, you can specify the range of IP addresses for your VPC using Classless Inter-Domain Routing (CIDR) notation. When you launch an instance (VM) in your VPC, you can assign a private IP address to the instance from this IP address range. If you don't explicitly assign a private IP address, one is assigned to the instance for you. 

**Public IP Addresses** 

By default, instances launched into the default subnet in your VPC receive a public IP address. This public IP address is assigned from a pool of public IP addresses, and is not associated with your account. This public IP address can't be manually added or removed from the VPC instance. The public IP address is mapped to the instance's private IP address using Network Address Translation (NAT). 

You can control whether or not your VPC instances get a public IP address by either enabling/disabling the public IP address attribute of the subnet, or by overriding the subnet's behavior when launching an instance into the VPC. 

If you want a persistent IP address for your VPC instance, you can use the `euca-allocate-address` to create an elastic IP address, and then use `euca-associate-address` to assign this address. 

**Subnets** 

Once you've created a VPC, you can create one or more subnets inside the VPC. A subnet is simply a logical subdivision of a network of IP addresses. Subnets can be used to enable tighter security, allow separate administration of the network by organization, and enable more efficient network traffic by containing traffic between nodes in a subnet and using route tables for traffic that needs to move between subnets. 

Note that subnets in a VPC cannot overlap; and the first four IP addresses and the last IP address are reserved for internal use. For example, of the 16 IP addresses of a /28 subnet, 11 are available for instances; of the 256 IP addresses of a /24 subnet, 251 are available for instances. Subnets must be larger than /28 and smaller than /16. 


{{% notice note %}}
For more information about subnets, see the on Wikipedia. 
{{% /notice %}}
