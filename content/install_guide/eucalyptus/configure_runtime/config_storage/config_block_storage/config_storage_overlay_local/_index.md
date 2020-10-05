+++
title = "Use the Overlay Local Filesystem"
weight = 10
+++

This topic describes how to configure the local filesystem as the block storage backend provider for the Storage Controller (SC).**Prerequisites** 

* Successful completion of all the install sections prior to this section. 
* The SC must be installed, registered, and running. 
* The local filesystem must have enough space to hold volumes and snapshots created in the cloud. 
* You must execute the steps below as a administrator. 
In this configuration the SC itself hosts the volume and snapshots for EBS and stores them as files on the local filesystem. It uses standard Linux iSCSI tools to serve the volumes to instances running on NCs. 

**To configure overlay block storage for the zone, run the following commands on the CLC** Configure the SC to use the local filesystem for EBS. 

    euctl ZONE.storage.blockstoragemanager=overlay 

The output of the command should be similar to: 

    one.storage.blockstoragemanager=overlay

Verify that the property value is now: 'overlay' 

    euctl ZONE.storage.blockstoragemanager

Your local filesystem (overlay) backend is now ready to use with Eucalyptus . 

