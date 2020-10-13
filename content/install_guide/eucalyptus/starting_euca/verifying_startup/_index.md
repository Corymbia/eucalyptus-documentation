+++
title = "Verify the Startup"
weight = 80
+++

At this point, all Eucalyptus services are enabled and starting up. Some of these services perform intensive initialization at start-up, particularly the first time they are started. You might have to wait a few minutes until they are fully operational. 

One quick way to determine if the components are running is to run netstat on the various hosts and look to see when the service ports are allocated to a process. Specifically, the CLC, Walrus, and the SC allocate ports 8773. The CC listens to port 8774, and the NC uses port 8775. 

Verify that everything has started without error. Expected outcomes include: 



* The CLC is listening on port 8773 
* Walrus is listening on port 8773 
* The SC is listening on port 8773 
* The CC is listening on port 8774 
* The NCs are listening on port 8775 
* Log files are being written to 
