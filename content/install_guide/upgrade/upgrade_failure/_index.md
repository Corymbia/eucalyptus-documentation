+++
title = "Downgrade a Failed Upgrade"
weight = 5
+++

If your upgrade fails, this topic describes how to downgrade your Eucalyptus cloud to an earlier release.
## Downgrade Overview
The upgrade process creates a backup to `/var/lib/eucalyptus/upgrade/eucalyptus.backup.TIMESTAMP` . For example: 


    /var/lib/eucalyptus/upgrade/eucalyptus.backup.1326905212

If the upgrade fails and needs to be reverted to your earlier version, you can find your preserved data in this directory. 

If the upgrade fails, all changes to the database and configuration files will be rolled back. You can retry the upgrade by following the upgrade instructions in the sections, [](upgrade_shutdown.dita) and [](upgrade_packages.dita) . 

If you do not want to continue with the upgrade after a failure, you can downgrade your installation back to the previous version. Note that downgrade instructions are different, depending on whether your Eucalyptus services are co-located or each hosted on their own machine. You will need to perform the downgrade for all services running on a single machine at the same time. 

The */var/lib/eucalyptus/db* and */var/lib/eucalyptus/keys* directories should not be affected by the upgrade. If they have been removed subsequent to the upgrade, you must restore the contents of these directories from your backups before downgrading. 

To downgrade from a failed upgrade, perform the tasks listed in the following sections. 


## Downgrade
You must [](upgrade_shutdown.dita) before downgrading Eucalyptus . Downgrade to the Eucalyptus 4.4.4 release package on each host machine: 
    yum downgrade 

Enter `y` when prompted, to downgrade the release package. 

If you have a Eucalyptus subscription, downgrade your subscription release package on each host machine to the release package you used for Eucalyptus 4.4.4 : 
    yum downgrade 

Enter `y` when prompted, to downgrade the subscription release package. 

Expire the cache for the yum repositories on each host machine: 
    yum clean expire-cache

Log in to each NC host and downgrade it: 
    yum downgrade eucalyptus eucalyptus-admin-tools eucalyptus-axis2c-common eucalyptus-blockdev-utils eucalyptus-imaging-toolkit eucalyptus-node eucanetd


{{% notice note %}}
The service name changed to in 4.3. 
{{% /notice %}}
Enter `y` when prompted, to downgrade the NC packages. 


{{% notice note %}}
Use the `yum shell` command for the following instructions. This will allow you to perform more complex transactions that are required for the downgrade. 


{{% /notice %}}
Log in to each machine running a Eucalyptus service and run the following command: 
    yum shell

Add the transaction commands listed below for each service installed on the machine host. If more than one service requires the same transactional command, you only need to specify that command once per machine host. Transaction commands for a combined machine host with CLC, Walrus, CC, and SC: 


    downgrade eucalyptus
    downgrade eucalyptus-admin-tools
    downgrade eucalyptus-axis2c-common
    downgrade eucalyptus-blockdev-utils
    downgrade eucalyptus-cluster 
    downgrade eucalyptus-cloud
    downgrade eucalyptus-common-java
    downgrade eucalyptus-common-java-libs
    downgrade eucalyptus-sc
    downgrade eucalyptus-service-image
    downgrade eucalyptus-walrus
    downgrade eucanetd


{{% notice note %}}
The service name changed to in 4.3. 
{{% /notice %}}
CLC transaction commands: 


    downgrade eucalyptus
    downgrade eucalyptus-admin-tools
    downgrade eucalyptus-axis2c-common
    downgrade eucalyptus-blockdev-utils
    downgrade eucalyptus-cloud
    downgrade eucalyptus-common-java
    downgrade eucalyptus-common-java-libs
    downgrade eucalyptus-service-image
    downgrade eucanetd

UFS transaction commands: 


    downgrade eucalyptus
    downgrade eucalyptus-admin-tools
    downgrade eucalyptus-cloud
    downgrade eucalyptus-common-java
    downgrade eucalyptus-common-java-libs

CC transaction commands: 


    downgrade eucalyptus
    downgrade eucalyptus-admin-tools
    downgrade eucalyptus-cluster 
    downgrade eucanetd


{{% notice note %}}
The service name changed to in 4.3. 
{{% /notice %}}
SC transaction commands: 


    downgrade eucalyptus
    downgrade eucalyptus-admin-tools
    downgrade eucalyptus-common-java
    downgrade eucalyptus-common-java-libs
    downgrade eucalyptus-sc

Walrus Backend transaction commands: 


    downgrade eucalyptus
    downgrade eucalyptus-admin-tools
    downgrade eucalyptus-common-java
    downgrade eucalyptus-common-java-libs
    downgrade eucalyptus-walrus

SAN 3PAR transaction commands: 


    downgrade eucalyptus-enterprise-storage-san-threepar
    downgrade eucalyptus-enterprise-storage-san-threepar-libs

SAN EqualLogic transaction commands: 


    downgrade eucalyptus-enterprise-storage-san-equallogic
    downgrade eucalyptus-enterprise-storage-san-equallogic-libs

SAN NetApp transaction commands: 


    downgrade eucalyptus-enterprise-storage-san-netapp
    downgrade eucalyptus-enterprise-storage-san-netapp-libs

When you have entered all the appropriate yum transaction commands, run the following command to verify that the transaction will be successful: 
    ts solve

Perform the downgrade by running the following command in the yum transaction shell: 
    run

Exit the yum transaction shell using the following command: 
    exit

Remove the */etc/eucalyptus/.upgrade* file from each Eucalyptus host machine: 
    rm /etc/eucalyptus/.upgrade

Enter `y` when prompted, to remove this file. 


{{% notice note %}}
Remove this file from every Eucalyptus host machine. 


{{% /notice %}}
Clear out the */var/run/eucalyptus/classcache/* directory on all Eucalyptus host machines: 
    rm -rf /var/run/eucalyptus/classcache/

This deletes 4.4 class file artifacts; they will be regenerated as needed for your downgraded cloud. 


## Downgrade Euca2ools
In general, there is no need to downgrade Euca2ools. 

Whenever you install Euca2ools, it will always give you the latest patch of a release (for example, you'd get 3.4.1 over 3.4.0). If, for example, you have 3.4.1 installed, then performing the following steps would downgrade to 3.4.0. 


{{% notice note %}}
If Euca2ools is not the source of upgrade failure, there is no reason to downgrade Euca2ools. 
{{% /notice %}}


Expire the cache for the yum repositories on each host machine: 
    yum clean expire-cache

Downgrade to Euca2ools 3.3.3 on each host machine: 
    yum downgrade euca2ools

Enter `y` when prompted, to downgrade Euca2ools. 


## Verify the Downgrade
Restart your downgraded cloud. Verify the Eucalyptus versions. For example: 
    # euca-version
    euca2ools 
    eucalyptus 

Verify that all services are `ENABLED` . 