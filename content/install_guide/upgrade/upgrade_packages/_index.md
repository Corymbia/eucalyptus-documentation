+++
title = "Upgrade Eucalyptus Package Repositories"
weight = 5
+++

This topic describes the steps to upgrade the Eucalyptus package repositories.**Prerequisites** See [](upgrade_prep.dita#upgrade_prep) for the complete list of upgrade prerequisites. 

You need to upgrade your existing Eucalyptus package repositories to use the new features in 4.4.5 . 


{{% notice note %}}
It's a good idea to upgrade all the non-NC's before the NCs. 
{{% /notice %}}


**To upgrade Eucalyptus** Enter the following command on each host machine that runs a Eucalyptus service: 
    yum install 

Review the dependencies and install package information. 

Enter `Y` when prompted to install the package. 

If you are not a Eucalyptus subscriber, skip this step. Install the Eucalyptus subscription package on each host that will run a Eucalyptus service: 
    yum install 

Review the dependencies and install package information. 

Enter `y` when prompted to install these packages. 

Enter the following command on each host machine that runs a Eucalyptus service: 
    yum clean all

Enter the following command on each host machine that runs a Eucalyptus service: 
    yum update 'eucalyptus*'

Enter `Y` when prompted to upgrade Eucalyptus . 

This retrieves the package verification keys; for more information, see [](installing_euca_software_signing.dita#installing_software_signing) . 

If you have previously customized your configuration files, `yum` returns a warning, and installs the new configuration files with a different name. This preserves your customizations. Before you continue, customize and rename the new Configuration files. 


{{% notice note %}}
For larger deployments, use a script to upgrade the host machines. For example: 
{{% /notice %}}
Perform the steps in [](../shared/console_upgrade_console.dita#console_upgrade_console) then return to this section. Enter the following command on each NC: 
    yum install qemu-kvm-ev

Review the Java dependency for any changes you might need to make after upgrading Eucalyptus packages. Java 8 is required as of Eucalyptus 4.3.0; previous releases of Eucalyptus used Java 7. See [](configure_java.dita#configure_java) . 

You are now ready to [](upgrade_start.dita) . 