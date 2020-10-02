+++
title = "Virtual Machine Types"
weight = 10
+++

A virtual machine type, known as a VM type, defines the number of CPUs, the size of memory, and the size of storage that is given to an instance when it boots. There are five pre-defined VM types in Eucalyptus. You can change the quantity of resources associated with each of the five VM types, but you cannot change the name of the VM types or the number of VM types available. If you customize the sizes they must be well-ordered. That means that the CPU, memory, and storage sizes of the next VM type must be equal to, or larger than, the size of the preceding VM type.  

The VM type used to instantiate an EMI must have a defined disk size larger than the EMI file. If a 6GB EMI is loaded into an instance with a VM type defined with a 5GB disk, it will fail to boot. The status of the instance will show as *pending* .  The pending status is the result of the fact that the Walrus cannot finish downloading the image to the Node Controller because the Node Controller has not allotted sufficient disk space for the download. Starting with Eucalyptus 3.2, if the user attempts to launch an instance with a VM type that is too small, they will receive an on-screen warning and the operation will terminate. 


## Available VM Types
Eucalyptus, like AWS, offers families of VM types. These families are composed of varying combinations of CPU, disk size, and memory. Eucalyptus offers enough VM types to give you the flexibility to choose the appropriate mix of resources for your applications. For the best experience, we recommend that you launch instance types that are appropriate for your applications. 



* This family includes the M1 and M3 VM types. These types provide a balance of CPU, memory, and network resources, which makes them a good choice for many applications. The VM types in this family range in size from one virtual CPU with two GB of RAM to eight virtual CPUs with 30 GB of RAM. The balance of resources makes them ideal for running small and mid-size databases, more memory-hungry data processing tasks, caching fleets, and backend servers. M1 types offer smaller instance sizes with moderate CPU performance. M3 types offer larger number of virtual CPUs that provide higher performance. We recommend you use M3 instances if you need general-purpose instances with demanding CPU requirements. 


* This family includes the C1 and CC2 instance types, and is geared towards applications that benefit from high compute power. Compute-optimized VM types have a higher ratio of virtual CPUs to memory than other families but share the NCs with non optimized ones. We recommend this type if you are running any CPU-bound scale-out applications. CC2 instances provide high core count (32 virtual CPUs) and support for cluster networking. C1 instances are available in smaller sizes and are ideal for scaled-out applications at massive scale. 
* This family includes the CR1 and M2 VM types and is designed for memory-intensive applications. We recommend these VM types for performance-sensitive database, where your application is memory-bound. CR1 VM types provide more memory and faster CPU than do M2 types. CR1 instances also support cluster networking for bandwidth intensive applications. M2 types are available in smaller sizes, and are an excellent option for many memory-bound applications. 
* This Micro family contains the T1 VM type. The t1.micro provides a small amount of consistent CPU resources and allows you to increase CPU capacity in short bursts when additional cycles are available. We recommend this type for lower throughput applications like a proxy server or administrative applications, or for low-traffic websites that occasionally require additional compute cycles. We do not recommend this VM type for applications that require sustained CPU performance. 
The following tables list each VM type Eucalyptus offers. Each type is listed in its associate VM family. 



| Instance Type | Virtual CPU | Disk Size | Memory | 
|  :---- |  :---- |  :---- |  :---- | 
| m1.small | 1 | 5 | 256 | 
| m1.medium | 1 | 10 | 512 | 
| m1.large | 2 | 10 | 512 | 
| m1.xlarge | 2 | 10 | 1024 | 
| m3.xlarge | 4 | 15 | 2048 | 
| m3.2xlarge | 4 | 30 | 4096 | 



| Instance Type | Virtual Cores | Disk Size | Memory | 
|  :---- |  :---- |  :---- |  :---- | 
| c1.medium | 2 | 10 | 512 | 
| c1.xlarge | 2 | 10 | 2048 | 
| cc1.4xlarge | 8 | 60 | 3072 | 
| cc2.8xlarge | 16 | 120 | 6144 | 



| Instance Type | Virtual Cores | Disk Size | Memory | 
|  :---- |  :---- |  :---- |  :---- | 
| m2.xlarge | 2 | 10 | 2048 | 
| m2.2xlarge | 2 | 30 | 4096 | 
| m2.4xlarge | 8 | 60 | 4096 | 
| cr1.8xlarge | 16 | 240 | 16384 | 



| Instance Type | Virtual Cores | Disk Size | Memory | 
|  :---- |  :---- |  :---- |  :---- | 
| t1.micro | 1 | 5 | 256 | 

