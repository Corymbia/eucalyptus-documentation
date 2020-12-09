+++
title = "System Requirements"
weight = 30
+++

To install Eucalyptus, your system must meet the baseline requirements described in this topic.

{{% notice note %}}
The specific requirements of your deployment, including the number of physical machines, structure of the physical network, storage requirements, and access to software are ultimately determined by the features you choose for your cloud and the availability of infrastructure required to support those features. 
{{% /notice %}}

## Compute Requirements

* Physical Machines: All services must be installed on physical servers, not virtual machines. 
* Central Processing Units (CPUs): We recommend that each host machine in your cloud contain either an Intel or AMD processor with a minimum of 4 2GHz cores. 
* Operating Systems: supports the following Linux distributions: CentOS 7.9 and RHEL 7.9. supports only 64-bit architecture. 
* Machine Clocks: Each host machine and any client machine clocks must be synchronized (for example, using NTP). These clocks must be synchronized all the time, not only during the installation process. 

## Storage and Memory Requirements

* Each machine needs a minimum of 100GB of storage.
* We recommend at least 500GB for Walrus and SC hosts.
* We recommend 200GB per NC host running Linux VMs. Note that larger available disk space enables a greater number of VMs. 
* Each machine needs a minimum of 16GB RAM. However, we recommend more RAM for improved caching and on NCs to support more instances. 

## Network Requirements

* For VPCMIDO, Eucalyptus needs MidoNet to be installed. 
* The network connecting machines that host components (except the CC and NC) must support UDP multicast for IP address 239.193.7.3. Note that UDP multicast is not used over the network that connects the CC to the NCs.

Once you are satisfied that your systems requirements are met, you are ready to plan your Eucalyptus installation. 

