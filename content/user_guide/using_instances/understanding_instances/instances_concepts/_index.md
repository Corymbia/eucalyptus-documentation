+++
title = "Instance Concepts"
weight = 10
+++

This section describes conceptual information to help you understand instances.
## Eucalyptus Machine Image (EMI)
A Eucalyptus machine image (EMI) is a copy of a virtual machine bootable file system stored in the Walrus storage. An EMI is a template from you can use to deploy multiple identical instances—or copies of the virtual machine. 

EMIs are analogous to Amazon Machine Images (AMIs) in AWS. In fact, you can download and deploy any of the 10,000+ AMIs as EMIs in a Eucalyptus cloud without significant modification. While it is possible to build your own EMI, it is might be just as simple to find a thoroughly vetted, freely available image in AWS, download it to your Eucalyptus cloud, and use that instead. 

When registered in a Eucalyptus cloud, each distinct EMI is given a unique ID for identification. The ID is in the format emi-<nnnnnnnn>. 

![image]({{< ref "/" >}}images/Eucalyptus-Machine-Images.png)

## Instance
A instance is a virtual machine deployed from an EMI. An instance then, is simply a running copy of an EMI, which means it always starts from a known baseline. There are two types of instances; instance store-backed and EBS-backed. This section describes store-backed instances. For information about EBS-backed instances, see [Using EBS]({{< ref using_block_storage.md >}}) . 

![image]({{< ref "/" >}}images/Instances-illustration.png)

Every instance receives a unique ID in the format i-<nnnnnnnn>. 

You can deploy multiple instances using a single command. In this case all the instances will have unique instance IDs but will share a common reservation ID. This reservation ID can be seen, for example, from the euca2ools `euca-describe-instances` command that lists running instances. Reservations IDs appear in the format r-<nnnnnnnn>. 

{{% notice note %}}
A *reservation* is an EC2 term used to describe the resources reserved for one or more instances launched in the cloud. 
{{% /notice %}}

## Persistence
Applications running in ephemeral instances that generate data that must be saved should write that data to some place other than the instance itself. There are two Eucalyptus options available. First, the data can be written to a volume that is attached to the instance. Volumes provided by the Storage Controller and attached to instances are persistent. Second, the data could be written to the Walrus using HTTP put/get operations. Walrus storage is also persistent. 

![image]({{< ref "/" >}}images/Persistence-in-Ephemeral-Instances.png)

If the application cannot be rewritten to send data to a volume or the Walrus, then the application should be deployed inside an EBS-backed instance. EBS-backed instances are persistent and operate in a manner more similar to a physical machine. 

