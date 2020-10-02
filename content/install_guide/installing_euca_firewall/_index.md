+++
title = "Install Eucalyptus from a Local Package Repository"
weight = 10
+++

This topic describes downloading and installing Eucalyptus from a local repository.In certain situations, you might need to install Eucalyptus from a local repository. For example if: 

* Your cloud is behind a firewall 
* Your change management requires a local repo 
* You have limited access to the Internet 
This procedure augments the standard installation instructions, and includes additional instructions for downloading and installing Eucalyptus from a local repository. 

**To install Eucalyptus from a local repository** 

Download the Eucalyptus repository to a local directory. For example: 
    wget -r --no-parent \ 
    http://downloads.eucalyptus.com/software/eucalyptus//rhel/7/x86_64/ \
    -P /tmp/eucalyptus 

Download Euca2ools: 
    wget -r --no-parent \
    http://downloads.eucalyptus.com/software/euca2ools//rhel/7/x86_64/ \
    -P /tmp/euca2ools 

In step 1 of the [existing installation instructions](installing_euca_release.dita) , modify the baseurl to point to your Eucalyptus local repository: 
    baseurl=file:///tmp/eucalyptus/downloads.eucalyptus.com/software/eucalyptus//rhel/7/x86_64

In step 2 of the [existing installation instructions](installing_euca_release.dita) , modify the baseurl to point to your local Euca2ools repository: 
    baseurl=file:///tmp/euca2ools/downloads.eucalyptus.com/software/euca2ools//rhel/7/x86_64

Run `yum update` . 