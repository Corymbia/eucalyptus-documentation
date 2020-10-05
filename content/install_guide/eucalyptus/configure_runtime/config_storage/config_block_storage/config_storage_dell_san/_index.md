+++
title = "Use a Dell EqualLogic SAN"
weight = 10
+++

This topic describes how to configure the Dell EqualLogic SAN as the block storage backend provider on the Storage Controller (SC).
{{% notice note %}}

{{% /notice %}}
**Prerequisites** 

* Successful completion of all the install sections prior to this section. 
* The SC must be installed, registered, and running. 
* You must have a paid subscription to in order to use a SAN backend. 
* You must have a functioning EqualLogic device available to cloud. 
* You must execute the steps below as a administrator. 
**To configure Dell EqualLogic block storage for the zone, run the following commands on the CLC** Configure the SC to use Equallogic for EBS. 

    euctl ZONE.storage.blockstoragemanager=equallogic

The output of the command should be similar to: 

    one.storage.blockstoragemanager=equallogic

Verify that the property value is now: 'equallogic' 

    euctl ZONE.storage.blockstoragemanager

Enable SAN support in Eucalyptus by entering your SAN's hostname or IP address, the username, password, and the name of the chap user: 

    euctl ZONE.storage.sanhost=SAN_IP_address 
    euctl ZONE.storage.sanuser=SAN_admin_user_name
    euctl ZONE.storage.sanpassword=SAN_admin_password 
    euctl ZONE.storage.chapuser=chap_username

(Optional) If your EqualLogic setup has dedicated paths for data access that are different from the management IP address supplied for the `ZONE.storage.sanhost` property, the following properties must also be configured in Eucalyptus : 

    euctl ZONE.storage.scpaths=data-IP-address ZONE.storage.ncpaths=data-IP-address

The SC and NC data IP address might be the same; or they can be different, if EqualLogic has multiple data interfaces. 

(Optional) These properties are available for EqualLogic thin provisioning, which can save significant space on your SAN. These properties take effect only during new EBS volume / snapshot creation. EBS volumes created from previously existing snapshots inherit the provisioning settings of the parent. 

    euctl -s ZONE.storage.eqlthin
    ZONE.storage.eqlthinprovision = Thin provision space on Equallogic SAN. Value must be true to enable and false to disable thin provisioning
    ZONE.storage.eqlthinminreserve = Minimum volume reserve for a thin-provisioned volume expressed as a % of the volume size. This is the amount of immediately writable, guaranteed space reserved for the volume
                        

Your Dell EqualLogic SAN backend is now ready to use with Eucalyptus . 