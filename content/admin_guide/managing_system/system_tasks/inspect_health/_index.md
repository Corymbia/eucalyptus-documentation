+++
title = "Inspect System Health"
weight = 10
+++

Eucalyptus provides access to the current view of service state and the ability to manipulate the state. You can inspect the service state to either ensure system health or to identify faulty services. You can modify a service state to maintain activities and apply external service placement policies.
## View Service State
Use the `euserv-describe-services` command to view the service state. The output indicates: 



* Component type of the service 
* Partition in which the service is registered 
* Unique name of the service 
* Current view of service state 
* Last reported epoch (this can be safely ignored) 
* Service URI 
* Fully qualified name of the service (This is needed for manipulating services that did not get unique names during registration. For example: internal services like DNS) 
The default output includes the services that are registered during configuration, as well as information about the DNS service, if present. You can obtain additional service state information, such as internal services, by providing the `-a` flag. 

You can also make requests to retrieve service information that is filtered by either: 



* current state (for example, ) 
* host where service is registered 
* partition where service is registered 
* type of service (for example, CC or Walrus) 
When you investigate service failures, you can specify `-events` to return a summary of the last fault. You can retrieve extended information (primarily useful for debugging) by specifying `-events -events-verbose` . 


## Heartbeat Service
`http://CLCIPADDRESS:8773/services/Heartbeat` provides a list of components and their respective statuses. This allows you to find out if a service is enabled without requiring cloud credentials. 


## Modify Service State
To modify a service: 

Enter the following command on the CLC, Walrus, or SC machines: 

    systemctl stop eucalyptus-cloud.service

On the CC, use the following command: 



    systemctl stop eucalyptus-cluster.service

If you want to shut down the SC for maintenance. The SC is `SC00` is `ENABLED` and needs to be `DISABLED` for maintenance. 

To stop `SC00` first verify that no volumes or snapshots are being created and that no volumes are being attached or detached, and then enter the following command on SC00: 



    systemctl stop eucalyptus-cloud.service

To check status of services, you would enter: 



    euserv-describe-services

When maintenance is complete, you can start the eucalyptus-cloud process on `SC00` , which will enter the `DISABLED` state by default. 



    systemctl start eucalyptus-cloud.service

Monitor the state of services using `euserv-describe-services` until `SC00` is `ENABLED` . 

