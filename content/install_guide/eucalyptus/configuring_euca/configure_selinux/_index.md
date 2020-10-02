+++
title = "Configure SELinux"
weight = 10
+++

We recommend enabling SELinux on host systems running Eucalyptus 4.4 services to improve their security on RHEL 7. Enabling SELinux, as described in this topic, can help contain break-ins. For more information, see [RedHat SELinux](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/SELinux_Users_and_Administrators_Guide/chap-Security-Enhanced_Linux-Troubleshooting.html) documentation. 

You need to set boolean values on Storage Controller (SC) and Management Console host machines. If your network mode is VPCMIDO, you also set a boolean value on the Cloud Controller (CLC) host machines. **To configure SELinux on Eucalyptus 4.4 :** 

On each Storage Controller (SC) host machine, run the following command: 
    setsebool -P eucalyptus_storage_controller 1

This allows Eucalyptus to manage EBS volumes. 

On each Management Console host machine, run the following command: 
    setsebool -P httpd_can_network_connect 1

This allows the Management Console's HTTP proxy to access the back end. 


{{% notice note %}}
If you can't access the console after starting it, this KB article might help: . 
{{% /notice %}}


If your cloud uses VPCMIDO networking mode, on the Cloud Controller (CLC), run the following command: 
    setsebool -P httpd_can_network_connect 1

This allows the CLC's HTTP proxy to access the back end. 

SELinux is now configured and ready to use with your Eucalyptus 4.4 cloud. 