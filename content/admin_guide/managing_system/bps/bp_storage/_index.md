+++
title = "Storage Volumes"
weight = 5
+++

Eucalyptus manages storage volumes for your private cloud. Volume management strategies are application specific, but this topic includes some general guidelines.When setting up your Storage Controller, consider whether performance (bandwidth and latency of read/write operations) or availability is more important for your application. For example, using several smaller volumes will allow snapshots to be taken on a rolling basis, decreasing each snapshot creation time and potentially making restore operations faster if the restore can be isolated to a single volume. However, a single larger volume allows for faster read/write operations from the VM to the storage volume. 

An appropriate network configuration is an important part of optimizing the performance of your storage volumes. For best performance, each Node Controller should be connected to a distinct storage network that enables the NC to communicate with the SC or SAN, without interfering with normal NC/VM-instance network traffic. 

Eucalyptus includes configurable limits on the size of a single volume, as well as the aggregate size of all volumes on an SC. The SC can push snapshots from the SAN device, where the volumes reside, to Walrus, where the snapshots become available across multiple clusters. Smaller volumes will be much faster to snapshot and transfer, whereas large volumes will take longer. However, if many concurrent snapshot requests are sent to the SC, operations may take longer to complete. 

Although an SC can manage an arbitrary number of volumes, intermittent issues have been reported with some hypervisors when attaching more than 16 volumes to a single NC. Where possible, limiting the number of volumes to no more than 16 per NC is advisable. 

EBS volumes are created from snapshots on the SC or SAN, after the snapshot has been downloaded from Walrus to the device. Creating an EBS volume from a snapshot on the same cluster as the source volume of the snapshot will reduce delays caused by having to transfer snapshots from Walrus. 

