+++
title = "Configure Object Storage"
weight = 5
chapter = true
+++


## Configure Object Storage
This topic describes how to configure object storage on the Object Storage Gateway (OSG) for the backend of your choice.The OSG passes requests to object storage providers and talks to the persistence layer (DB) to authenticate requests. You can use Walrus, Riak CS, or Ceph-RGW as the object storage provider. 



* **Walrus** - the default backend provider. It is a single-host Eucalyptus -integrated provider which provides basic object storage functionality for the small to medium scale. Walrus is intended for light S3 usage. 




* - an open source scalable general purpose data platform created by Basho Technologies. It is intended for deployments which have heavy S3 usage requirements where a single-host system like Walrus would not be able to serve the volume of operations and amount of data required. 




* - an object storage interface built on top of Librados to provide applications with a RESTful gateway to Ceph Storage Clusters. Ceph-RGW uses the Ceph Object Gateway daemon (radosgw), which is a FastCGI module for interacting with a Ceph Storage Cluster. Since it provides interfaces compatible with OpenStack Swift and Amazon S3, the Ceph Object Gateway has its own user management. Ceph Object Gateway can store data in the same Ceph Storage Cluster used to store data from Ceph Filesystem clients or Ceph Block Device clients. The S3 and Swift APIs share a common namespace, so you may write data with one API and retrieve it with the other. 

{{% notice note %}}

{{% /notice %}}


You must configure the OSG to use one of the backend provider options. 


{{% notice note %}}
If OSG has been registered but not yet properly configured, it will be listed in the state when listed with the euserv-describe-services command. For example: 
{{% /notice %}}

    [root@g-26-03 ~]# euserv-describe-services --show-headers --filter service-type=objectstorage
    SERVICE  TYPE              	ZONE    	NAME                   	  STATE	
    SERVICE  objectstorage      user-api-1  user-api-1.objectstorage  broken

