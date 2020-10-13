+++
title = "Register the Node Controllers"
weight = 50
+++

This topic describes how to register a Node Controller (NC) with a Cluster Controller (CC).

**Prerequisites** 

* The Cluster Controller service must be properly installed and started. 
* The Node Controller service must be properly installed and started. 
* If you are upgrading, you should understand that: 
  * If you're upgrading an NC, just register that NC (on the CC that had it registered before).
  * If you're upgrading the set of non-NC host machines, register all the NCs (on each CC that had NCs registered).



**To register the Node Controller service with the Eucalyptus cloud**

SSH to the Cluster Controller in the zone. On the CC, register all NCs using the following command with the IP address of each NC host machine:

    clusteradmin-register-nodes node0_IP_address ... [nodeN_IP_address]

For example: 

    clusteradmin-register-nodes 10.111.5.160 10.111.5.161 10.111.5.162

Copy the CC's security credentials using the following command: 

    clusteradmin-copy-keys node0_IP_address ... [nodeN_IP_address]

For example: 

    clusteradmin-copy-keys 10.111.5.160 10.111.5.161 10.111.5.162

Repeat the steps for each zone in your cloud. The registered Node Controller service is now ready for your cloud. 

