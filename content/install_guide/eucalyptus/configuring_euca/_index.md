+++
title = "Configure Eucalyptus"
weight = 5
chapter = true
+++


# Configure Eucalyptus
The first launch of Eucalyptus is different than a restart of a previously running Eucalyptus deployment in that it sets up the security mechanisms that will be used by the installation to ensure system integrity. 

Eucalyptus configuration is stored in a text file, */etc/eucalyptus/eucalyptus.conf* , that contains key-value pairs specifying various configuration parameters. Eucalyptus reads this file when it launches and when various forms of reset commands are sent it the Eucalyptus components. 


{{% notice note %}}
Perform the following tasks after you install software, but before you start the services. 
{{% /notice %}}


{{% children %}}
