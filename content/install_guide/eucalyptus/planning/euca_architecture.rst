+++
title = "Eucalyptus Architecture Overview"
weight = 5
+++

..  _euca_architecture:

This topics describes the relationship of the components in a Eucalyptus installation.

.. image:: {{< ref "/" >}}images/euca_arch_separate_hosts.png

The cloud components: Cloud Controller (CLC) and Walrus, as well as user components: User-Facing Services (UFS) and the Management Console, communicate with cluster components: the Cluster Controllers (CCs) and Storage Controllers (SCs). The CCs and SCs, in turn, communicate with the Node Controllers (NCs). The networks between machines hosting these components must be able to allow TCP connections between them. 

However, if the CCs are on separate subnets (one for the network on which the cloud components are hosted and another for the network that NCs use) the CCs will act as software routers between these networks in some networking configurations. Each cluster can use an internal private network for its NCs, and the CCs can route traffic from that private network to a network shared by the cloud components. 

Virtual machines (VMs) run on the machines that host NCs. You can use the CCs as software routers for traffic between clients outside Eucalyptus and VMs. Or the VMs can use the routing framework already in place without CC software routers. However, depending on the layer-2 isolation characteristics of your existing network, you might not be able to implement all of the security features supported by Eucalyptus . 

Riak CS clusters provide an alternative to Walrus as an object storage provider. SAN clusters, available to Eucalyptus subscribers, are alternatives to direct-attached storage and Ceph as block storage providers. 

