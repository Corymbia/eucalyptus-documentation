+++
title = "Using EBS-Backed Instances"
weight = 10
hidden = true
+++

An EBS-backed instance is very much like a physical machine in the way it boots and persists data.  Because an EBS-backed instance functions in a manner similar to physical machine, it makes it a good choice to run legacy applications that cannot be re-architected for the cloud.  




![image]({{< ref "/" >}}images/Using-EBS-Instances.png)


EBS-backed instances provide a workaround for the 10GB size limit for instance store-backed EMI images.  This is particularly important for Windows instances which can easily exceed 10GB in size. EBS-backed instances have a maximum size of 1TB. 

An EBS-backed boot volume can still be protected by taking a snapshot of it.  In fact, other non-boot volumes can be attached to the EBS-backed instance and they can be protected using snapshots too. 

