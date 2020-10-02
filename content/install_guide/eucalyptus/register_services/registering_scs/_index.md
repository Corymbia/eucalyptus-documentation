+++
title = "Register the Storage Controller"
weight = 5
+++

This topic describes how to register a Storage Controller (SC) with the Cloud Controller (CLC).**Prerequisites** 

* The Cloud Controller must be properly installed and started. 
* The Storage Controller service must be properly installed and started. 
**To register the Storage Controller service with the Eucalyptus cloud** Copy the security credentials from the CLC to each machine running Storage Controller services. Run this command on the CLC host machine: 
    clcadmin-copy-keys -z ZONE HOST

For example: 


    clcadmin-copy-keys -z zone-1 10.111.5.182

On the CLC host machine, run the following command: 
    euserv-register-service -t storage -h IP -z ZONE SVCINSTANCE

where: 



* is the IP address of the SC you are registering with this CLC. 
* name should be a descriptive name for the zone controlled by the CC. For example: . An SC must have the same name as the CC in the same zone. 
* must be a unique name for the SC service. We recommend that you use a short-hand name of the IP address or hostname of the machine, for example: or . 

{{% notice note %}}
We recommend that you use IP addresses instead of DNS names when registering services. 
{{% /notice %}}
For example: 


    euserv-register-service -t storage -h 10.111.5.182 -z zone-1 sc-10.111.5.182


{{% notice note %}}
The SC automatically goes to the state after being registered with the CLC; it will remain in that state until you explicitly configure the SC by configuring the backend storage provider (later). For more information, see . 
{{% /notice %}}
Repeat the above steps for each Storage Controller in each zone. Verify that the Storage Controller service is registered with the following command: 
    euserv-describe-services SVCINSTANCE

The registered Storage Controller service is now ready for your cloud. 

