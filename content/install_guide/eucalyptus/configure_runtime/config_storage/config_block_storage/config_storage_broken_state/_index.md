+++
title = "About the BROKEN State"
weight = 10
+++

This topic describes the initial state of the Storage Controller (SC) after you have registered it with the Cloud Controller (CLC).The SC automatically goes to the `broken` state after being registered with the CLC; it will remain in that state until you explicitly configure the SC by telling it which backend storage provider to use. 

You can check the state of a storage controller by running `euserv-describe-services --expert` and note the state and status message of the SC(s). The output for an unconfigured SC looks something like this: 



    SERVICE	storage        	ZONE1        	SC71           	BROKEN    	37  	http://192.168.51.71:8773/services/Storage	arn:euca:eucalyptus:ZONE1:storage:SC71/
    SERVICEEVENT	6c1f7a0a-21c9-496c-bb79-23ddd5749222	arn:euca:eucalyptus:ZONE1:storage:SC71/
    SERVICEEVENT	6c1f7a0a-21c9-496c-bb79-23ddd5749222	ERROR
    SERVICEEVENT	6c1f7a0a-21c9-496c-bb79-23ddd5749222	Sun Nov 18 22:11:13 PST 2012
    SERVICEEVENT	6c1f7a0a-21c9-496c-bb79-23ddd5749222	SC blockstorageamanger not configured. Found empty or unset manager(unset). Legal values are: das,overlay,ceph



Note the error above: `SC blockstoragemanager not configured. Found empty or unset manager(unset). Legal values are: das,overlay,ceph` . 

This indicates that the SC is not yet configured. It can be configured by setting the `ZONE.storage.blockstoragemanager` property to 'das', 'overlay', or 'ceph'. 

You can verify that the configured SC block storage manager using: 

    euctl ZONE.storage.blockstoragemanager

to show the current value.

