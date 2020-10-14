+++
title = "Plan Services Placement"
weight = 30
+++


![image]({{< ref "/" >}}images/euca_deploy_examples_training_source.png)

## Cloud Services
The main decision for cloud services is whether to install the Cloud Controller (CLC) and Walrus on the same server. If they are on the same server, they operate as separate web services within a single Java environment, and they use a fast path for inter-service communication. If they are not on the same server, they use SOAP and REST to work together. 

Sometimes the key factor for cloud services is not performance, but server cost and data center configuration. If you only have one server available for the cloud, then you have to install the services on the same server. 

All services should be in the same data center. They use aggressive time-outs to maintain system responsiveness so separating them over a long-latency, lossy network link will not work. 


## User Services
The User Facing Services (UFS) handle all of the AWS APIs and provide an entry point for clients and users interacting with the Eucalyptus cloud. The UFS and the Management Console are often hosted on the same machine since both must be accessible from the public, client-facing network. 

You may optionally choose to have redundant UFS and Management Console host machines behind a load balancer. 


## Zone Services
The Eucalyptus services deployed in the zone level of a Eucalyptus deployment are the Cluster Controller (CC) and Storage Controller (SC). 

You can install all zone services on a single server, or you can distribute them on different servers. The choice of one or multiple servers is dictated by the demands of user workload in terms of number of instances (CC) and EBS volume access (SC). 

Things to consider for CC placement: 



* Place the CC on a server that has TCP/IP connectivity to the front-end servers and the NC servers in its zone. 
* Each CC can manage a maximum of 4000 instances. 
Things to consider for SC placement: 



* The SC host machine must always have TCP/IP connectivity to the CLC and be able use multicast to the CLC. 
* The SC must have TCP/IP connectivity to the UFS/OSG hosts for uploading snapshots into the object store. (The SC does not require connectivity directly to users, it is an internal component and does not serve user EBS API requests; that job is done by the UFS.) 
* The SC must be reachable via TCP/IP from all NCs in the zone within which the SC is registered. The SC and NC exchange tokens to authorize volume attachment, so they must be able to directly communicate. The SC provides the NCs with network access to the dynamic block volumes on the SC's storage (if the SC is configured for overlay local filesystem or DAS-JBOD). 
* IF using Ceph the SC must also have TCP/IP connectivity to the Ceph cluster.
* If you are going to use overlay local filesystem or DAS-JBOD configurations to export local SC storage for EBS, then SC storage should consist of a fast, reliable disk pool (either local file-system or block-attached storage) so that the SC can create and maintain volumes for the NCs. The capacity of the disk pool should be sufficient to provide the NCs with enough space to accommodate all dynamic block volumes requests from end users. 

## Node Services
The Node Controllers are the services that comprise the Eucalyptus backend. All NCs must have network connectivity to whatever machine(s) host their EBS volumes. Hosts are either a Ceph deployment or the SC.

