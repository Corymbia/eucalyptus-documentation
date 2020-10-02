+++
title = "SAN Support"
weight = 10
hidden = true
+++


{{% notice note %}}

{{% /notice %}}
SAN support extends the functionality of the Eucalyptus Storage Controller (SC) to provide a high performance data conduit between VMs running in Eucalyptus and attached SAN devices. Eucalyptus dynamically manages SAN storage without the need for the administrator to manually allocate and de-allocate storage, manage snapshots or set up data connections. 


![image]({{< ref "/" >}}images/euca-arch-extras-one-cluster.png)
Eucalyptus with SAN support allows you to: 



* Integrate block storage functionality (dynamic block volumes, snapshots, creating volumes from snapshots, etc.) with existing SAN devices 
* Link VMs in the cloud directly to SAN devices, thereby removing I/O communication bottlenecks of the physical hardware host 
* Incorporate enterprise-level SAN features (high-speed, large-capacity, reliability) to deliver a production-ready EBS (block storage) solution for the enterprise 
To use Eucalyptus with supported SAN storage, you must decide whether administrative access can be provided to Eucalyptus to control the SAN. If this is possible in your environment, Eucalyptus can automatically and dynamically manage SAN storage. 

Eucalyptus supports these SAN devices: 



* HP 3PAR SAN 
* NetApp SAN 
* Dell EqualLogic SAN 
See the Compatibility Matrix in the Release Notes for supported versions. 

