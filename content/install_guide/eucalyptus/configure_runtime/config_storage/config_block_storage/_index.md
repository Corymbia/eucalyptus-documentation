+++
title = "Configure Block Storage"
weight = 5
chapter = true
+++


# Configure Block Storage
This topic describes how to configure block storage on the Storage Controller (SC) for the backend of your choice.

The Storage Controller (SC) provides functionality similar to the Amazon Elastic Block Store (Amazon EBS). The SC can interface with various storage systems. Eucalyptus block storage (EBS) exports storage volumes that can be attached to a VM and mounted or accessed as a raw block device. EBS volumes can persist past VM termination and are commonly used to store persistent data. 

Eucalyptus provides the following open source (free) backend providers for the SC: 

* Overlay, using the local file system
* DAS-JBOD (just a bunch of disks) 
* Ceph

You must configure the SC to use one of the backend provider options. 

{{% children %}}
