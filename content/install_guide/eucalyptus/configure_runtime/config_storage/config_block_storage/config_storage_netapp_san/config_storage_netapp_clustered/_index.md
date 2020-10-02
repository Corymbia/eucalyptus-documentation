+++
title = "Enable NetApp Clustered Data ONTAP"
weight = 5
+++

This topic describes how to configure the NetApp Clustered Data ONTAP SAN block storage backend for the Storage Controller (SC).**Prerequisites** 

* Successful completion of all the install sections prior to this section. 
* The SC must be installed, registered, and running. 
* You must have a paid subscription to in order to use a SAN backend. 
* You must have a functioning NetApp Clustered Data ONTAP device available to cloud. 
* You must have a data Vserver with one or more aggregates and iSCSI protocol for storing and retrieving and data. 
* Vserver user with administrator privileges to the specific Vserver should be set up and made available to . 
* FlexClone and iSCSI licenses must be enabled on the setup. 
* Management (only) Logical Interface (LIF) should be configured for the Vserver and an IP address or hostname is assigned to it. 
* Data LIFs should be configured on the Vserver. 
* One or more aggregates with necessary capacity is assigned to the Vserver. 
* Network connectivity: 
* You must execute the steps below as a administrator. 
For more information on NetApp Clustered Data ONTAP, see [NetApp Clustered Data ONTAP: An Introduction](http://www.netapp.com/us/system/pdf-reader.aspx?m=tr-3982.pdf&cc=us) . 

**To configure NetApp Clustered Data ONTAP block storage for the zone, run the following commands on the CLC** Configure the SC to use NetApp for EBS: 
    euctl ZONE.storage.blockstoragemanager=netapp

The output of the command should be similar to: 


    ZONE.storage.blockstoragemanager=netapp

Verify that the property value is now: 'netapp' 
    euctl ZONE.storage.blockstoragemanager 

Wait for the SC to transition to 'notready' or 'disabled' states. On the CLC, enable NetApp SAN support in Eucalyptus by entering the Vserver's hostname or IP address, the username and password of the administrator account, CHAP username and Vserver name. 
{{% notice note %}}
uses Challenge Handshake Authentication Protocol (CHAP) for disk operations. The CHAP username can be any value, however it should be unique when sharing a NetApp Vserver across multiple clusters. 
{{% /notice %}}

{{% notice note %}}
CHAP support for NetApp was added in 3.3. The SC will not transition to ENABLED state until the CHAP username is conﬁgured. 
{{% /notice %}}

    euctl ZONE.storage.sanhost=Vserver_IP_address 
    euctl ZONE.storage.sanuser=Vserver_admin_username 
    euctl ZONE.storage.sanpassword=Vserver_admin_password 
    euctl ZONE.storage.chapuser=Chap_username


{{% notice note %}}
The following command may fail if tried immediately after conﬁguring the block storage manager. Retry the command a few times, pausing for a few seconds after each retry: 
{{% /notice %}}

    euctl ZONE.storage.vservername=Vserver_name

Wait for the SC to transition to ENABLED state. 
{{% notice note %}}
The SC must be in the ENABLED state before configuring the following properties. 
{{% /notice %}}
If no aggregate is set, Eucalyptus will query the NetApp Vserver for all available aggregates and use the one that has the highest capacity (free space) by default. To make Eucalyptus use specific aggregate(s) configure the following property: 
    euctl ZONE.storage.aggregate=aggregate_1_name, aggregate_2_name,...

If you want Eucalyptus to use the smallest aggregate first configure the following property: 


    euctl ZONE.storage.uselargestaggregate=false

Set an IP address for the iSCSI data LIF on the ENABLED CLC. This is used for NCs performing disk operations on the Vserver. 
    euctl ZONE.storage.ncpaths=IP

Set an IP address for the iSCSI data LIF on the ENABLED CLC. This is used by the SC for performing disk operations on the Vserver. The SC connects to the data LIFs on the Vserver in order to transfer snapshots to objectstorage during snapshot operations. 
    euctl ZONE.storage.scpaths=IP

Your NetApp Clustered Data ONTAP SAN backend is now ready to use with Eucalyptus . 