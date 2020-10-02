+++
title = "Update the Service Images"
weight = 10
hidden = true
+++

This topic describes how to update the service images after the Eucalyptus software upgrade.As of Eucalyptus 4.2.0, service images are templates for imaging workers, load balancers, and database images, all using the same service image. 

Install the imaging worker image. Run the following command on the machine where you installed the Eucalyptus imaging worker image: 
    esi-install-image --install-default


{{% notice note %}}
If you use the parameter on this command, do not specify localhost (as in user@localhost); the command will fail with an error. Use the region name as shown in a Euca2ools configuration file such as . For example, if these lines are shown in that file: Add the following, if you use the parameter: 
{{% /notice %}}
Your Eucalyptus 4.4 upgrade is now complete. 