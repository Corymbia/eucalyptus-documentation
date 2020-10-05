+++
title = "Use Direct Attached Storage (JBOD)"
weight = 10
+++

This topic describes how to configure the DAS-JBOD as the block storage backend provider for the Storage Controller (SC).**Prerequisites** 

* Successful completion of all the install sections prior to this section. 
* The SC must be installed, registered, and running. 
* Direct Attached Storage requires that have enough space for locally cached snapshots. 
* You must execute the steps below as a administrator. 
**To configure DAS-JBOD block storage for the zone, run the following commands on the CLC** Configure the SC to use the Direct Attached Storage for EBS. 

    euctl ZONE.storage.blockstoragemanager=das

The output of the command should be similar to: 

    one.storage.blockstoragemanager=das

Verify that the property value is now: 'das' 

    euctl ZONE.storage.blockstoragemanager

Set the DAS device name property. The device name can be either a raw device (/dev/sdX, for example), or the name of an existing Linux LVM volume group. 

    euctl ZONE.storage.dasdevice=DEVICE_NAME

For example: 



    euctl one.storage.dasdevice=/dev/sdb

Your DAS-JBOD backend is now ready to use with Eucalyptus . 