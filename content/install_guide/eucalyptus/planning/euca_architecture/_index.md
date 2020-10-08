+++
title = "Eucalyptus Architecture Overview"
weight = 10
+++

This topics describes the relationship of the components in a Eucalyptus installation.
![image]({{< ref "/" >}}images/euca_arch_separate_hosts.png)
The cloud components: Cloud Controller (CLC) and Walrus, as well as user components: User-Facing Services (UFS) and the Management Console, communicate with cluster components: the Cluster Controllers (CCs) and Storage Controllers (SCs). The CCs and SCs, in turn, communicate with the Node Controllers (NCs). The networks between machines hosting these components must be able to allow TCP connections between them. 

Ceph provides an alternative to Walrus as an object storage provider, and can also be used as a block storage provider (EBS). 
