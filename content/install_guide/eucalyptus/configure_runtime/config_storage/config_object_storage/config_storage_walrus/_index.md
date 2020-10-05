+++
title = "Use Walrus Backend"
weight = 10
+++

This topic describes how to configure Walrus as the object storage backend provider for the Object Storage Gateway (OSG).**Prerequisites** 

* Successful completion of all the install sections prior to this section. 
* The UFS must be registered and enabled. 
* You must execute the steps below as a administrator. 
**To configure Walrus object storage for the OSG** Enter `walrus` as the storage provider using the `euctl` command. 

    euctl objectstorage.providerclient=walrus

Check that the OSG is enabled. 

    euserv-describe-services

If the state appears as `disabled` or `broken` , check the cloud-*.log files in the */var/log/eucalyptus* directory. A `disabled` state generally indicates that there is a problem with your network or credentials. See [Log File Location and Content]({{< ref ts_logs.md >}}) for more information. 

The Walrus backend and OSG are now ready for production. 

