+++
title = "Configure Object Storage"
weight = 5
+++


This topic describes how to configure object storage on the Object Storage Gateway (OSG) for the backend of your choice. The OSG passes requests to object storage providers and talks to the persistence layer (DB) to authenticate requests. You can use Walrus, MinIO, or Ceph-RGW as the object storage provider.

* **Walrus** - the default backend provider. It is a single-host Eucalyptus -integrated provider which provides basic object storage functionality for the small scale. Walrus is intended for light S3 usage.

* **MinIO** - a high performing scalable object storage provider. MinIO implements the S3 API which is used by the OSG, not directly by end users. Distributed MinIO provides protection against multiple node/drive failures and bit rot using erasure code.

* **Ceph-RGW** - an object storage interface built on top of Librados to provide applications with a RESTful gateway to Ceph Storage Clusters. Ceph-RGW uses the Ceph Object Gateway daemon (radosgw), which is a FastCGI module for interacting with a Ceph Storage Cluster. Since it provides interfaces compatible with OpenStack Swift and Amazon S3, the Ceph Object Gateway has its own user management. Ceph Object Gateway can store data in the same Ceph Storage Cluster used to store data from Ceph Filesystem clients or Ceph Block Device clients. The S3 and Swift APIs share a common namespace, so you may write data with one API and retrieve it with the other. 

You must configure the OSG to use one of the backend provider options. 

{{% notice note %}}
If OSG has been registered but not yet properly configured, it will be listed in the state when listed with the euserv-describe-services command.
{{% /notice %}}


Example showing unconfigured *objectstorage*:

```bash
# euserv-describe-services --show-headers --filter service-type=objectstorage
SERVICE  TYPE              	ZONE    	NAME                   	  STATE	
SERVICE  objectstorage      user-api-1  user-api-1.objectstorage  broken
```


{{% children sort="weight" %}}
