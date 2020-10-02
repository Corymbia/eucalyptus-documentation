+++
title = "Use Riak CS"
weight = 10
hidden = true
+++

This topic describes how to configure Riak CS as the object storage backend provider for the Object Storage Gateway (OSG).**Prerequisites** 

* Successful completion of all the install sections prior to this section. 
* The UFS must be registered and enabled. 
* You must have a functioning Riak CS cluster. 
* You must execute the steps below as a administrator. 
For more information on Riak CS, see the [Riak documentation](https://github.com/basho/basho_docs/tree/master/content/riak) . 

**To configure Riak CS object storage for the OSG** Enter `riakcs` as the storage provider using the `euctl` command. 
    euctl objectstorage.providerclient=riakcs

Specify the RiakCS/S3 endpoint that you want to use with Eucalyptus . For example: 
    euctl objectstorage.s3provider.s3endpoint=riakcs-01.riakcs-cluster.myorg.com

Provide your RiakCS credentials to access your RiakCS installation: 
    euctl objectstorage.s3provider.s3accesskey=RIAK_CS_ACCESS_KEY_ID
    euctl objectstorage.s3provider.s3secretkey=RIAK_CS_SECRET_ACCESS_KEY

After successful configuration, check to ensure that the state of the OSG is `enabled` by running the `euserv-describe-services` command. For example: 
    [root@g-26-03 ~]# euserv-describe-services --show-headers --filter service-type=objectstorage
    SERVICE  TYPE              	ZONE    	NAME                   	  STATE	
    SERVICE  objectstorage      user-api-1  user-api-1.objectstorage  enabled 

If the state appears as `disabled` or `broken` , check the cloud-*.log files in the */var/log/eucalyptus* directory. A `disabled` state generally indicates that there is a problem with your network or credentials. See [](../troubleshooting-guide/ts_logs.dita#ts_logs) for more information. 

The Riak CS backend and OSG are now ready for production. 

