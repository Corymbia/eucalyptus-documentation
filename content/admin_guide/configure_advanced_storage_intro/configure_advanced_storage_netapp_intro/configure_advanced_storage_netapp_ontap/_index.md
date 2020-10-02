+++
title = "NetApp Clustered Data ONTAP"
weight = 10
+++

A clustered ONTAP system consists of two or more individual NetApp storage controllers with attached disks. The basic building block is the HA pair, a term familiar from Data ONTAP 7G or 7-Mode environments.An HA pair consists of two identical controllers; each controller actively provides data services and has redundant cabled paths to the other controller’s disk storage. 

One of the key differentiators in a clustered ONTAP environment is that multiple HA pairs are combined together into a cluster to form a shared pool of physical resources available to applications. The shared pool appears as a single system image for management purposes. This means there is a single common point of management, whether through GUI or CLI tools, for the entire cluster. While the members of each HA pair must be the same controller type, the cluster can consist of heterogeneous HA pairs. Each NetApp storage controller with in a cluster is also referred to as a node. 

The primary logical cluster component is the Virtual Storage Server, known as Vserver. Clustered ONTAP supports from one to hundreds of Vservers in a single cluster. A Vserver is configured for the client and host access protocols (such as iSCSI). Each Vserver contains at least one volume and at least one logical interface. The accessing hosts and clients connect to the Vserver using a logical interface (or LIF). LIFs present an IP address which will be used by iSCSI hosts. Each LIF has a home port on a NIC or HBA. LIFs are used to virtualize the NIC and HBA ports rather than mapping IP addresses or WWNs directly to the physical ports. Each Vserver requires its own dedicated set of LIFs, and up to 128 LIFs can be defined on any cluster node. 

Each Vserver consists of different volumes and LIFs, providing secure compartmentalized access. Although the volumes and LIFs in each Vserver share the same physical resources (network ports and storage aggregates), a host or client can only access the data in a Vserver through a LIF defined in that Vserver. Administrative controls make sure that a delegated administrator with access to a Vserver can only see the logical resources assigned to that Vserver. 

For more information on NetApp Clustered Data ONTAP, see [Clustered Data ONTAP 8.1 and 8.1.1: An Introduction](http://www.netapp.com/us/system/pdf-reader.aspx?m=tr-3982.pdf&cc=us) . 

Eucalyptus integrates with NetApp Clustered ONTAP system by operating against a Vserver. SC must be conﬁgured to operate against Vserver contained in the NetApp Clustered ONTAP environment. SCs in other Eucalyptus clusters can be conﬁgured to use the same or different Vservers. SC and NC only interact with the conﬁgured Vserver and do not communicate with the Clustered ONTAP interfaces directly. 

