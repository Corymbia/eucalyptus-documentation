+++
title = "Use Walrus Backend"
weight = 30
+++

This topic describes how to configure Walrus as the object storage backend provider for the Object Storage Gateway (OSG).

## Prerequisites

* Successful completion of all the install sections prior to this section. 
* The UFS must be registered and enabled. 

## To configure Walrus object storage

You must execute the steps below as a administrator. 

Configure **walrus** as the storage provider using the *euctl* command. 

```bash
euctl objectstorage.providerclient=walrus
```

Check that the OSG is enabled. 

```bash
euserv-describe-services
```

If the state appears as **disabled** or **broken** , check the cloud-*.log files in the */var/log/eucalyptus* directory. A **disabled** state generally indicates that there is a problem with your network or credentials. See [Log File Location and Content]({{< ref ts_logs.md >}}) for more information.

The Walrus backend and OSG are now ready for production. 
