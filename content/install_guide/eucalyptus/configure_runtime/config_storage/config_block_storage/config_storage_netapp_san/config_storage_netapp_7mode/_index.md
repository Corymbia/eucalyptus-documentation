+++
title = "Enable NetApp 7-mode"
weight = 5
+++

This topic describes how to configure the NetApp 7-mode SAN block storage backend for the Storage Controller (SC).**Prerequisites** 

* Successful completion of all the install sections prior to this section. 
* The SC must be installed, registered, and running. 
* You must have a paid subscription to in order to use a SAN backend. 
* You must have a functioning NetApp 7-mode device available to cloud. 
* A supported version of the Data ONTAP operating system must be installed on the SAN. 
* FlexClone and iSCSI licenses must be enabled on the setup. 
* One or more aggregates with sufficient space should be available and iSCSI service should be started. 
* Administrator account credentials for NetApp Filer must be available to be configured in . 
* You must execute the steps below as a administrator. 
**To configure NetApp 7-mode SAN block storage for the zone, run the following commands on the CLC** Configure the SC to use the Netapp for EBS. 
    euctl ZONE.storage.blockstoragemanager=netapp

The output of the command should be similar to: 
    ZONE.storage.blockstoragemanager=netapp

Verify that the property value is now: 'netapp' 
    euctl ZONE.storage.blockstoragemanager

Wait for the SC to transition to the 'notready' or 'disabled' state. On the CLC, enable NetApp SAN support in Eucalyptus by entering the Filer's hostname or IP address, the username and password of the administrator account, and CHAP username. 
{{% notice note %}}
uses Challenge Handshake Authentication Protocol (CHAP) for disk operations. The CHAP username can be any value, however it should be unique when sharing a NetApp Filer across multiple clusters. 
{{% /notice %}}

{{% notice note %}}
CHAP support for NetApp was added in 3.3. An SC will not transition to ENABLED state until the CHAP username is conﬁgured. 
{{% /notice %}}

    euctl ZONE.storage.sanhost=Filer_IP_address 
    euctl ZONE.storage.sanuser=Filer_admin_username
    euctl ZONE.storage.sanpassword=Filer_admin_password 
    euctl ZONE.storage.chapuser=Chap_username

Wait for the SC to transition to the ENABLED state. 
{{% notice note %}}
The SC must be in the ENABLED state before configuring the following properties. 
{{% /notice %}}
If no aggregate is set, Eucalyptus will query the NetApp Filer for all available aggregates and use the one that has the highest capacity (free space) by default. To make Eucalyptus use specific aggregate(s) configure the following property: 
    euctl ZONE.storage.aggregate=aggregate_1_name,aggregate_2_name,...

If you want Eucalyptus to use the smallest aggregate first configure the following property: 


    euctl ZONE.storage.uselargestaggregate=false

Set the iSCSI data IP on the ENABLED CLC. This IP is used by NCs to perform disk operations on the Filer. 
{{% notice note %}}
Filer IP address can be used as the data port IP. If this is not set, will automatically use the Filer IP address/hostname. 
{{% /notice %}}

{{% notice note %}}
does not support Multipath I/O for NetApp 7-mode Filers. 
{{% /notice %}}

    euctl ZONE.storage.ncpaths=IP

Set the iSCSI data IP on the ENABLED CLC. This IP is used by the SC to perform disk operations on the Filer. The SC connects to the Filer in order to transfer snapshots to objectstorage during snapshot operations. 
{{% notice note %}}
The Filer IP address can be used as the data port IP. If this is not set, will automatically use the Filer IP address/hostname. 
{{% /notice %}}

{{% notice note %}}
does not support Multipath I/O for NetApp 7-mode Filers. 
{{% /notice %}}

    euctl ZONE.storage.scpaths=IP

Your NetApp 7-mode SAN backend is now ready to use with Eucalyptus . 