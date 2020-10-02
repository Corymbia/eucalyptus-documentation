+++
title = "Upgrade Euca2ools Package Repositories"
weight = 10
hidden = true
+++

This topic describes the steps to upgrade the Euca2ools package repositories.**Prerequisites** See [](upgrade_prep.dita#upgrade_prep) for the complete list of upgrade prerequisites. 

It is recommended (but optional) that you upgrade Euca2ools to the version compatible with Eucalyptus 4.4.5 . If you do not install the new version of Euca2ools, you will not be able to use new features from the command line. 

**To upgrade Euca2ools** 

Enter the following command on each host machine that runs a Eucalyptus service or uses Euca2ools: 
    yum install 

Review the dependencies and install package information. 

Enter `Y` when prompted to install the package. 

Enter the following command on each host machine that runs a Eucalyptus service or uses Euca2ools: 
    yum clean expire-cache

Enter the following command on each host machine that runs a Eucalyptus service or uses Euca2ools: 
    yum update euca2ools

Enter `Y` when prompted to upgrade Euca2ools. 

This retrieves the package verification keys; for more information, see [](installing_euca_software_signing.dita#installing_software_signing) . 

Repeat these steps for each host machine that runs a Eucalyptus service. You are now ready to [](upgrade_packages.dita) . 