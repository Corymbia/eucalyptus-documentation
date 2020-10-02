+++
title = "Eucalyptus Components"
weight = 5
+++

This topic describes the various components that comprise a Eucalyptus cloud.The following image shows a high-level architecture of Eucalyptus with its main components. 


![image]({{< ref "/" >}}images/euca_cloud_arch_basics.png)
A detailed description of each Eucalyptus component follows. 


## Cloud Controller
In many deployments, the Cloud Controller (CLC) service and the User-Facing Services (UFS) are on the same host machine. This server is the entry-point into the cloud for administrators, developers, project managers, and end-users. The CLC handles persistence and is the backend for the UFS. A Eucalyptus cloud must have exactly one CLC. 


## User-Facing Services
The User-Facing Services (UFS) serve as endpoints for the AWS-compatible services offered by Eucalyptus : EC2 (compute), AS (AutoScaling), CW (CloudWatch), ELB (LoadBalancing), IAM (Euare), and STS (tokens). A Eucalyptus cloud can have several UFS host machines. 


## Object Storage Gateway
The Object Storage Gateway (OSG) is part of the UFS. The OSG passes requests to object storage providers and talks to the persistence layer (DB) to authenticate requests. You can use Walrus, Riak CS, or Ceph-RGW as the object storage provider. 


## Object Storage Provider
The Object Storage Provider (OSP) can be either the Eucalyptus Walrus backend, Riak CS, or Ceph-RGW. Walrus is intended for light S3 usage and is a single service. [Riak](https://github.com/basho/riak) is an open source scalable general purpose data platform; it is intended for deployments with heavy S3 usage. Ceph-RGW is an object storage interface built on top of Librados. 


{{% notice note %}}

{{% /notice %}}

## Management Console
The Eucalyptus Management Console is an easy-to-use web-based interface that allows you to manage your Eucalyptus cloud. The Management Console is often deployed on the same host machine as the UFS. A Eucalyptus cloud can have multiple Management Console host machines. 


## Cluster Controller
The Cluster Controller (CC) service must run on a host machine that has network connectivity to the host machines running the Node Controllers (NCs) and to the host machine for the CLC. CCs gather information about a set of NCs and schedules virtual machine (VM) execution on specific NCs. All NCs associated with a single CC must be in the same subnet. 


## Storage Controller
The Storage Controller (SC) service provides functionality similar to Amazon Elastic Block Store (Amazon EBS). The SC can interface with various storage systems. Elastic block storage exports storage volumes that can be attached by a VM and mounted or accessed as a raw block device. EBS volumes can persist past VM termination and are commonly used to store persistent data. An EBS volume cannot be shared between multiple VMs at once and can be accessed only within the same availability zone in which the VM is running. Users can create snapshots from EBS volumes. Snapshots are stored by the OSG and made available across availability zones. Eucalyptus with SAN support provides the ability to use your enterprise-grade SAN devices to host EBS storage within a Eucalyptus cloud. 


## Node Controller
The Node Controller (NC) service runs on any machine that hosts VM instances. The NC controls VM activities, including the execution, inspection, and termination of VM instances. It also fetches and maintains a local cache of instance images, and it queries and controls the system software (host OS and the hypervisor) in response to queries and control requests from the CC. 


## Eucanetd
The eucanetd service implements artifacts to manage and define Eucalyptus cloud networking. Eucanetd runs alongside the CLC or NC services, depending on the configured networking mode. 

