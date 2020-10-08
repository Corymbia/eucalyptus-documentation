+++
title = "Eucalyptus Overview"
weight = 10
+++

Eucalyptus is open source software for building AWS-compatible private and hybrid clouds. As an Infrastructure as a Service product, Eucalyptus allows you to flexibly provision your own collections of resources (both compute and storage), on an as-needed basis.


## Who Should Read this Guide?
This guide is for Eucalyptus users who wish to run application workloads on a Eucalyptus cloud. 


## What’s in this Guide?
This guide contains instructions for users of the Eucalyptus cloud platform. While these instructions apply generally to all tools capable of interacting with Eucalyptus, such as the Eucalyptus Management Console or the AWS S3 toolset, but the primary focus is on the use of Euca2ools (Eucalyptus command line tools). The following is an overview of the contents of this guide. 



| How do I …? | Related Topic | 
|  :---- |  :---- | 
| Begin using and configuring Eucalyptus | [getting_started]({{< relref "getting_started" >}}) | 
| Run and control with virtual machine (VM) instances | [using_instances]({{< relref "using_instances" >}}) | 
| Use Eucalyptus’ elastic block storage | [using_block_storage]({{< relref "using_block_storage" >}}) | 
| Apply tags and filters | [resource_and_tags]({{< relref "resource_and_tags" >}}) | 
| Manage access for groups and users | [using_access]({{< relref "using_access" >}}) | 
| Understand the Eucalyptus VM networking and security features | [networking_security]({{< relref "networking_security" >}}) | 
| Use Eucalyptus’ Auto Scaling features | [autoscaling_intro]({{< relref "autoscaling_intro" >}}) | 
| Use elastic load balancing | [elb_intro]({{< relref "elb_intro" >}}) | 
| Generate metrics about my cloud | [using_monitoring]({{< relref "using_monitoring" >}}) | 
| Use scalable object storage | [osg_using]({{< relref "osg_using" >}}) | 
| Use CloudFormation | [cf_overview]({{< relref "cf_overview" >}}) | 
| Use Virtual Private Cloud | [vpc_intro]({{< relref "vpc_intro" >}}) | 


## Eucalyptus Features
Eucalyptus offers ways to implement, manage, and maintain your own collection of virtual resources (machines, network, and storage). The following is an overview of these features. 

### AWS API compatibility
Eucalyptus provides API compatibility with Amazon Web Services, to allow you to use familiar tools and commands to provision your cloud. 

### Block- and bucket-based storage abstractions
Eucalyptus provides storage options compatible with Amazon's EBS (block-based) and S3 (bucket-based) storage products. 

### Self-service capabilities
Eucalyptus offers a Management Console, allowing your users to request the resources they need, and automatically provisioning those resources where available. 

### Web-based Interface
The Eucalyptus Management Console is accessible from any device via a browser. The Console initial page provides a Dashboard view of components available to you to manage, configure, provision, and generate various reports. 


## Resource Management
Eucalyptus offers tools to seamlessly manage a variety of virtual resources. The following is an overview of the types of resources your cloud platform. 

### SSH Key Management
Eucalyptus employs public and private keypairs to validate your identity when you log into VMs using SSH. You can add, describe, and delete keypairs. 

### Image Management
Before running instances, someone must prepare VM images for use in the cloud. This can be an administrator or a user. Eucalyptus allows you to bundle, upload, register, describe, download, unbundle, and deregister VM images. 

### Linux Guest OS Support
Eucalyptus lets you run your own VMs in the cloud. You can run, describe, terminate, and reboot a wide variety of Linux-based VMs that were prepared using image management commands. 

### IP Address Management
Eucalyptus can allocate, associate, disassociate, describe, and release IP addresses. Depending on the networking mode, you might have access to public IP addresses that are not statically associated with a VM ( Elastic IPs ). Eucalyptus provides tools to allow users to reserve and dynamically associate these elastic IPs with virtual machines. 

### Security Group Management
Security groups are sets of firewall rules applied to VMs associated with the group. Eucalyptus lets you create, describe, delete, authorize, and revoke security groups. How much of these things can a typical user actually do? 

### Volume and Snapshot Management
Eucalyptus allows you to create dynamic block volumes. A dynamic block volume is similar to a raw block storage device that can be used with virtual machines. You can create, attach, detach, describe, bundle, and delete volumes. You can also create and delete snapshots of volumes and create new volumes from snapshots. 

