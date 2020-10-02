+++
title = "System Requirements"
weight = 10
hidden = true
+++

To install Eucalyptus , your system must meet the baseline requirements described in this topic.
{{% notice note %}}
The specific requirements of your deployment, including the number of physical machines, structure of the physical network, storage requirements, and access to software are ultimately determined by the features you choose for your cloud and the availability of infrastructure required to support those features. 
{{% /notice %}}

## Compute Requirements


* Physical Machines: All services must be installed on physical servers, not virtual machines. 
* Central Processing Units (CPUs): We recommend that each host machine in your cloud contain either an Intel or AMD processor with a minimum of 4 2GHz cores. 
* Operating Systems: supports the following Linux distributions: CentOS 7 and RHEL 7. supports only 64-bit architecture. 
* Machine Clocks: Each host machine and any client machine clocks must be synchronized (for example, using NTP). These clocks must be synchronized all the time, not only during the installation process. 
* Machine Access: Verify that all machines in your network allow SSH login, and that root or sudo access is available on each of them. 

## Storage and Memory Requirements


* Each machine in your network needs a minimum of 160GB of storage. 
* We recommend at least 500GB for Walrus and SC hosts running Linux VMs. We recommend at least 250GB for Walrus and SC hosts running Windows VMs. 
* We recommend 160GB per NC host running Linux VMs, and at least 250GB per NC host for running Windows VMs. Note that larger available disk space enables a greater number of VMs. 
* Each machine in your network needs a minimum of 8GB RAM. However, we recommend more RAM for improved caching. 
* Host machines running multiple services (e.g., CLC, CC and SC) likely need more than the minimum amounts of RAM and storage. 

## Network Requirements


* All NCs must have access to a minimum of 1Gb Ethernet network connectivity. 
* All components must have at least one Network Interface Card (NIC) for a base-line deployment. For better network isolation and scale, the CC should have two NICs (one facing the CLC/user network and one facing the NC/VM network). 
* For networking mode, needs at least one existing network. 
* For , needs Midokura Enterprise MidoNet to be installed. For more information, see . 
* The network connecting machines that host components (except the CC and NC) must support UDP multicast for IP address 239.193.7.3. Note that UDP multicast is not used over the network that connects the CC to the NCs. For information about testing connectivity, see . 
Once you are satisfied that your systems requirements are met, you are ready to plan your Eucalyptus installation. 

