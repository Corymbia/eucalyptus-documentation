+++
title = "Understanding Eucalyptus EDGE Mode"
weight = 5
+++

In EDGE networking mode, the components responsible for implementing Eucalyptus VM networking artifacts are running at the edge of a Eucalyptus deployment: the Linux host machines acting as Node Controllers (NCs). On each NC host machine, a Eucalyptus stand-alone service, eucanetd, runs side-by-side with the NC service. The eucanetd service receives dynamically changing Eucalyptus networking views and is responsible for configuring the Linux networking subsystem to reflect the latest view. 

EDGE networking mode integrates with your existing network infrastructure, allowing you to inform Eucalyptus , through configuration parameters for EDGE mode, about the existing network, which Eucalyptus then will consume when implementing the networking view. 

EDGE networking mode integrates with two basic types of pre-existing network setups: 



* One flat IP network used to service component systems, VM public IPs (elastic IPs), and VM private IPs. 
* Two networks, one for components and VM public IPs, and the other for VM private IPs. 

{{% notice note %}}
EDGE networking mode integrates with networks that already exist. If the network, netmask, and router don't already exist, you must create them outside before configuring EDGE mode. 
{{% /notice %}}

## EDGE Mode Requirements


* Each NC host machine must have an interface configured with an IP on a VM public and a VM private network (which can be the same network). 
* There must be IP connectivity from each NC host machine (where eucanetd runs) and the CLC host machine, so that network path from instances to the metadata server (running on the CLC host machine) can be established. 
* There must be a functioning router in place for the private network. This router will be the default gateway for VM instances. 
* The private and public networks can be the same network, but they can also be separate networks. 
* The NC host machines need a bridge configured on the private network, with the bridge interface itself having been assigned an IP from the network. 
* If you're using a public network, the NC host machines need an interface on the public network as well (if the public and private networks are the same network, then the bridge needs an IP assigned on the network). 
* If you run multiple zones, each zone can use the same network as its private network, or they can use separate networks as private networks. If you use separate networks, you need to have a router in place that is configured to route traffic between the networks. 
* If you use private addressing only, the CLC host machine must have a route back to the VM private network. 

## EDGE Mode Limitations


* Global network updates (such as security group rule updates, security group VM membership updates, and elastic IP updates) are applied through an "eventually consistent" mechanism, as opposed to an "atomic" mechanism. That is, there may be a brief period of time where one NC has the new state implemented but another NC has the previous state implemented. 
* Mappings between VM MAC addresses and private IPs are strictly enforced. This means that instances cannot communicate using addresses the cloud has not assigned to them. 
