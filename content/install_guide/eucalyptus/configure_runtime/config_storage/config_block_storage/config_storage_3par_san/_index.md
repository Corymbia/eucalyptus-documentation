+++
title = "Use an HP 3PAR SAN"
weight = 5
chapter = true
+++


## Use an HP 3PAR SAN
This topic describes how to configure the HP 3PAR SAN as the block storage backend provider for the Storage Controller (SC).
{{% notice note %}}

{{% /notice %}}
**Prerequisites** 

* Successful completion of all the install sections prior to this section. 
* The SC must be installed, registered, and running. 
* You must have a paid subscription to in order to use a SAN backend. 
* You must have a functioning 3PAR device available to cloud. 
* Network access must be available from the: 


* Verify this 3PAR device checklist: 


* You must execute the steps below as a administrator. 
**To configure HP 3PAR SAN block storage for the zone, run the following commands on the CLC** Configure the SC to use the 3PAR for EBS. 
    euctl ZONE.storage.blockstoragemanager=threepar

The output of the command should be similar to: 
    one.storage.blockstoragemanager=threepar

Verify that the property value is now: 'threepar' 
    euctl ZONE.storage.blockstoragemanager

On the CLC, enable SAN support in Eucalyptus by entering your SAN's hostname or IP address, the username, password, and the paths: 
    euctl ZONE.storage.sanhost=3PAR_IP_address 
    euctl ZONE.storage.sanuser=3PAR_admin_user_name 
    euctl ZONE.storage.sanpassword=3PAR_admin_password 
    euctl ZONE.storage.scpaths=3PAR_iSCSI_IP 
    euctl ZONE.storage.ncpaths=3PAR_iSCSI_IP

If you have multiple management IP addresses for the SAN adapter, provide a comma-delimited list of IP addresses to the `ZONE.storage.sanhost` property. 

Assign any string to the `chap_username` property. 
    euctl ZONE.storage.chapuser=chap_username

Assign the 3PAR CPG that should be used for creating virtual volumes to the `threeparusercpg` property. 
    euctl ZONE.storage.threeparusercpg=3PAR_user_cpg

Assign the 3PAR CPG that should be used for creating virtual volume snapshot space to the `threeparcopycpg` property. 
    euctl ZONE.storage.threeparcopycpg=3PAR_copy_cpg

(Optional) These properties are available for advanced configuration. 
    euctl ZONE.storage.threepar
    PROPERTY        one.storage.threepardomain     {}
    DESCRIPTION     one.storage.threepardomain     Name of the virtual domain containing threeparusercpg and threeparcopycpg. If threeparusercpg and threeparcopycpg don't belong to a specific virtual domain leave this property unset
    
    PROPERTY        one.storage.threeparmultihostaccess     false
    DESCRIPTION     one.storage.threeparmultihostaccess     Configure multi host access to virtual volume. Value must be true to enable multi host access. Default value is false
    
    PROPERTY        one.storage.threeparoptimizesnaptovol     true
    DESCRIPTION     one.storage.threeparoptimizesnaptovol     If set to true, snapshot to volume creation path is optimized. If set to false, volume to snapshot path is optimized. Default value is true
    
    PROPERTY        one.storage.threeparpersona     2
    DESCRIPTION     one.storage.threeparpersona     Persona (integer value) to be used when exporting a VLUN to host. Default value is 2 and represents a Linux initiator
    
    PROPERTY        one.storage.threeparphysicalcopytimeout     120
    DESCRIPTION     one.storage.threeparphysicalcopytimeout     Time duration in minutes to wait for physical copy operation to complete. Default value is 120
    
    PROPERTY        one.storage.threeparusetpvv     true
    DESCRIPTION     one.storage.threeparusetpvv     Configure virtual volumes to be either thinly (TPVV) or fully provisioned (FPVV). Value must be true for TPVV and false for FPVV. Default value is true
    
    PROPERTY        one.storage.threeparvluncachesize     10000
    DESCRIPTION     one.storage.threeparvluncachesize     Maximum number of VLUNs that can be cached by the provider. Default value is 10000

For more information about the `threeparoptimizesnaptovol` property, and how to configure it, see [About Operation Mode Optimization](../install-guide/config_storage_3par_op_modes.dita#op_modes) . 

Your 3PAR SAN backend is now ready to use with Eucalyptus . 