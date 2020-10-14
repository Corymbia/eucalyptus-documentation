+++
title = "Configure the Firewall"
weight = 10
+++


## Restricting Network Access
This section provides basic guidance on setting up a firewall around your Eucalyptus components. It is not intended to be exhaustive. 

On the Cloud Controller (CLC), Walrus, and Storage Controller (SC), allow for the following jGroups traffic: 



* TCP connections between CLC, user-facing services (UFS), object storage gateway (OSG), Walrus, and SC on port 8779 (or the first available port in range 8779-8849) 
* UDP connections between CLC, UFS, OSG, Walrus, and SC on port 7500 
* Multicast connections between CLC and UFS, OSG, Walrus, and SC to IP 239.193.7.3 on UDP port 8773 
On the UFS, allow the following connections: 



* TCP connections from end-users and instances on ports 8773 
* End-user and instance connections to DNS ports 
On the CLC, allow the following connections: 



* TCP connections from UFS, CC and Eucalyptus instances (public IPs) on port 8773 (for metadata service) 
* TCP connections from UFS, OSG, Walrus, and SC on port 8777 
On the CC, make sure that all firewall rules are compatible with the dynamic changes performed by Eucalyptus, described in the section below. Also allow the following connections: 



* TCP connections from CLC on port 8774 
On OSG, allow the following connections: 



* TCP connections from end-users and instances on port 8773 
* TCP connections from SC and NC on port 8773 
On Walrus, allow the following connections: 



* TCP connections from OSG on port 8773 
On the SC, allow the following connections: 



* TCP connections from CLC and NC on TCP port 8773 
* TCP connections from NC on TCP port 3260, if tgt (iSCSI open source target) is used for EBS in DAS or Overlay modes 
On the NC, allow the following connections: 



* TCP connections from CC on port 8775 
* TCP connections from other NCs on port 16514 
* DHCP traffic forwarding to VMs 
* Traffic forwarding to and from instances' private IP addresses 
