+++
title = "Understanding VPCMIDO and MidoNet"
weight = 10
+++

This topic describes MidoNet components and their Eucalyptus deployment options, which provide support for VPC on Eucalyptus. Eucalyptus VPCMIDO mode resembles the Amazon Virtual Private Cloud (VPC) product wherein the network is fully configurable by users. In Eucalyptus, it is implemented with a Software-Defined Networking (SDN) technology called MidoNet. MidoNet is a network virtualization platform for Infrastructure-as-a-Service (IaaS) clouds that implements and exposes virtual network components as software abstractions, enabling programmatic provisioning of virtual networks. 

This network mode requires configuration of MidoNet in order to make cloud networking functional. It offers the most advanced networking capabilities and therefore it is recommended to be used on all new Eucalyptus installations. 


## MidoNet Components
A MidoNet deployment consists of four types of nodes (according to their logical functions or services offered), connected via four IP networks as depicted in Figure 1. MidoNet does not require any specific hardware, and can be deployed in commodity x86_64 servers. Interactions with MidoNet are accomplished through Application Programming Interface (API) calls, which are translated into (virtual) network topology changes. Network state information is stored in a logically centralized data store, called the Network State Database (NSDB), which is implemented on top of two open-source distributed coordination and data store technologies: ZooKeeper and Cassandra. Implementation of (virtual) network topology is realized via cooperation and coordination among MidoNet agents, which are deployed in nodes that participate in MidoNet. 


![image]({{< ref "/" >}}images/euca_mido_1v2.png)
*Figure 1: Logical view of a MidoNet deployment. Four components are connected via four networks.* 

Node types: 

* MidoNet Network State Database (NSDB): consists of a cluster of ZooKeeper and Cassandra. All MidoNet nodes must have IP connectivity with NSDB. 
* MidoNet API: consists of MidoNet web app. Exposes MidoNet REST APIs. 
* Hypervisor: MidoNet agent (Midolman) are required in all Hypervisors to enable VMs to be connected via MidoNet overlay networks/SDN. 
* Gateway: Gateway nodes are connected to the public network, and enable the network flow from MidoNet overlays to the public network. 

Physical Networks: 

* NSDB: IP network that connects all nodes that participate in MidoNet. While NSDB and Tunnel Zone networks can be the same, it is recommended to have an isolated (physical or VLAN) segment. 
* API: in deployments only eucanetd/CLC needs access to the API network. Only "special hosts/processes" should have access to this network. The use of "localhost" network on the node running CLC/eucanetd is sufficient and recommended in deployments. 
* Tunnel Zone: IP network that transports the MidoNet overlay traffic ( VM traffic), which is not "visible" on the physical network. 
* Public network: network with access to the Internet (or corporate/enterprise) network. 


## MidoNet Deployment Scale
Three reference architectures are presented in this document, ordered by complexity and size:

* Proof-of-Concept (PoC)
* Production: Small
* Production: Large

Production: Large reference architecture represents the most complete and recommended deployment model of MidoNet for Eucalyptus. Whenever possible (such as when resources are available), deployments should closely match with the Production: Large reference architecture (even on small scale clouds).

All MidoNet components are designed and implemented to horizontally scale. Therefore, it is possible to start small and add resources as they become available.


## Eucalyptus with MidoNet
A Eucalyptus with MidoNet deployment consists of the following components: 

![image]({{< ref "/" >}}images/euca_mido_2.png)
*Figure 2: Logical view of a Eucalyptus with MidoNet deployment. VM private network is created/virtualized by MidoNet, and 'software-defined' by eucanetd. Ideally, each component and network should have its own set of independent resources. In practice, components are grouped and consolidated into a set of servers, as detailed in different reference architectures.* 

MidoNet components, Eucalyptus components, and three extra networks are present. 


## Proof of Concept (PoC)
The PoC reference architecture is designed for very small and transient workloads, typical in development and testing environments. Quick deployment with minimal external network requirements are the key points of PoC reference architecture. 

**Requirements** 

Servers: 

* Four (4) or more modern Intel cores or AMD modules - exclude logical cores that share CPU resources from the count (Hyperthreads and AMD cores within a module) 
* 2GB of RAM reserved for MidoNet Agent (when applicable) 
* 4GB of RAM reserved for MidoNet NSDB (when applicable) 
* 4GB of RAM reserved for MidoNet API (when applicable) 
* 30GB of free disk space for NSDB (when applicable) 

Physical Network: 

* One (1) 1Gbps IP Network 
* A range or list of public IP addresses (Euca_public_IPs) 
* Internet Gateway 

Limits: 

* Ten (10) MidoNet agents (i.e., 1 Gateway node, 1 CLC, and 8 NCs) 
* One (1) MidoNet Gateway 
* No fail over, fault tolerance, and/or network load balancing/sharing 

**Deployment Topology** 

* Single server with all MidoNet components (NSDB, API, and Midolman), and with CLC/eucanetd 
* A server acting as MidoNet Gateway - when BGP terminated links are used, this node must not be co-located with CLC/eucanetd (in a proxy_arp setup described below, it is possible to consolidate CLC/eucanetd with MidoNet Gateway). This is due to incompatibilities in CentOS/RHEL7 netns (used by eucanetd), and bgpd (started by Midolman when BGP links are configured). 
* Hypervisors with Midolman 
* One IP network handling NSDB, Tunnel Zone, and Public Network traffic 
* API communication via loopback/localhost network 

![image]({{< ref "/" >}}images/euca_mido_3v2.png)
*Figure 3: PoC deployment topology. A single IP network carries NSDB, Tunnel Zone, and Public Network traffic. A single server handles MidoNet NSDB, API (and possibly Gateway) functionality.* 

**MidoNet Gateway Bindings** 

Three ways to realize MidoNet Gateway bindings are discussed below, starting with the most recommended setup. 

Public CIDR block(s) allocated for Eucalyptus (Euca_Public_IPs) needs to be routed to MidoNet Gateway by the customer network - this is an environment requirement, outside of control of both MidoNet and Eucalyptus systems. One way to accomplish this is to have a BGP terminated link available. MidoNet Gateway will establish a BGP session with the customer router to: (1) advertise Euca_Public_IPs to the customer router; and (2) get the default route from the customer router. 

If a BGP terminated link is not available, but the routing of Euca_Public_IPs is delegated to MidoNet Gateway (configuration of customer routing infrastructure), similar setup can be used. In such scenario, static routes are configured on the customer router (to route Euca_Public_IPs to MidoNet Gateway), and on MidoNet (to use the customer router as the default route). 


![image]({{< ref "/" >}}images/euca_mido_4.png)
*Figure 4: How servers are bound to MidoNet in a PoC deployment with BGP. A BGP terminated link is required: the gateway node eth device is bound to MidoNet virtual router (when BGP is involved, the MidoNet Gateway and Eucalyptus CLC cannot be co-located). Virtual machine tap devices are bound to MidoNet virtual bridges.* 

If routed Euca_Public_IPs are not available, static routes on all involved nodes (L2 connectivity is required among nodes) can be used as illustrated below. 


![image]({{< ref "/" >}}images/euca_mido_5.png)
*Figure 5: How servers are bound to MidoNet in a PoC deployment without routed Euca_Public_IPs. Clients that need communication with Euca_Public_IPs configure static routes using MidoNet Gateway as the router. MidoNet Gateway configures a static default route to customer router.* 

In the case nodes outside the public network broadcast domain (L2) needs to access Euca_Public_IPs, a setup using proxy_arp, as illustrated below, can be used. 


![image]({{< ref "/" >}}images/euca_mido_6.png)
*Figure 6: How servers are bound to MidoNet in a PoC deployment with proxy_arp. When routed Euca_Public_IPs are not available, the gateway node should proxy arp for public IP addresses allocated for Eucalyptus , and forward to a veth device that is bound to a MidoNet virtual router. Virtual machine tap devices are bound to MidoNet virtual bridges.* 


## Production: Small
The Production: Small reference architecture is designed for small scale production quality deployments. It supports MidoNet NSDB fault tolerance (partial failures), and limited MidoNet Gateway failover and load balancing/sharing. 

Border Gateway Protocol (BGP) terminated uplinks are recommended for production quality deployments. 

**Requirements** 

Servers: 

* Four (4) or more modern Intel cores or AMD modules - exclude logical cores that share CPU resources from the count (Hyperthreads and AMD cores within a module) - for gateway nodes, 4 or more cores should be dedicated to MidoNet agent (Midolman) 
* 4GB of RAM reserved for MidoNet Agent (when applicable), 8GB for Gateway nodes 
* 4GB of free RAM reserved for MidoNet NSDB (when applicable) 
* 4GB of free RAM reserved for MidoNet API (when applicable) 
* 30GB of free disk space for NSDB (when applicable) 
* Two (2) 10Gbps NICs per server 
* Three (3) servers dedicated to MidoNet NSDB 
* Two (2) servers as MidoNet Gateways 

Physical Network: 

* One (1) 10Gbps IP Network for public network (if upstream links are 1Gbps, this could be 1Gbps) 
* One (1) 10Gbps IP Network for Tunnel Zone and NSDB 
* Public Classless Inter-Domain Routing (CIDR) block (Euca_public_IPs) 
* Two (2) BGP terminated uplinks 

Limits: 

* Thirty two (32) MidoNet agents (i.e., 2 Gateway nodes and 30 Hypervisors) 
* Two (2) MidoNet Gateways 
* Tolerate 1 NSDB server failure 
* Tolerate 1 MidoNet Gateway/uplink failure 
* Limited uplinks load sharing/balancing 

**Deployment Topology** 

* A 3-node cluster for NSDB (co-located ZooKeeper and Cassandra) 
* eucanetd co-located with MidoNet API Server 
* Two (2) MidoNet Gateway Nodes 
* Hypervisors with Midolman 
* One 10Gbps IP network handling NSDB and Tunnel Zone traffic 
* One 10Gbps IP Network handling Public Network traffic 
* API communication via loopback/localhost network 

![image]({{< ref "/" >}}images/euca_mido_7v2.png)
*Figure 7: Production:Small deployment topology. A 10Gbps IP network carries NSDB and Tunnel Zone traffic. Another 10Gbps IP network carries Public Network traffic. A 3-node cluster for NSDB tolerates 1 server failure, and 2 gateways enable network failover and limited load balancing/sharing.* 


![image]({{< ref "/" >}}images/euca_mido_8.png)
*Figure 8: How servers are bound to MidoNet in a Production:Small deployment. Gateway Nodes have physical devices bound to a MidoNet virtual router. These devices should have L2 and L3 connectivity to the Customer's Router, and with BGP terminated links. Virtual machine tap devices are bound to MidoNet virtual bridges.* 

**NSDB Data Replication** 

* NSDB is deployed in a cluster of 3 nodes 
* ZooKeeper and Cassandra both have built-in data replication 
* One server failure is tolerated 

**MidoNet Gateway Failover** 

* Two paths are available to and from MidoNet, and failover is handled by BGP 

**MidoNet Gateway Load Balancing and Sharing** 

* Load Balancing from MidoNet is implemented by MidoNet agents (Midolman): ports in a stateful port group with default routes out are used in a round-robin fashion. 
* Partial load sharing from the Customer's router to MidoNet can be accomplished by: 


## Production: Large
The Production:Large reference architecture is designed for large scale (500 to 600 MidoNet agents) production quality deployments. It supports MidoNet NSDB fault tolerance (partial failures), and MidoNet Gateway failover and load balancing/sharing. 

Border Gateway Protocol (BGP) terminated uplinks are required. Each uplink should come from an independent router. 

**Requirements:** 

* Eight (8) or more modern Intel cores or AMD modules - exclude logical cores that share CPU resources from the count (Hyperthreads and AMD cores within a module) - for gateway nodes, 8 or more cores should be dedicated to MidoNet agent (Midolman) 
* 4GB of RAM reserved for MidoNet Agent (when applicable), 16GB for Gateway nodes 
* 4GB of free RAM reserved for MidoNet NSDB (when applicable) 
* 4GB of free RAM reserved for MidoNet API (when applicable) 
* 30GB of free disk space for NSDB (when applicable) 
* One 1Gbps and 2 10Gbps NICs per server 
* Five (5) servers dedicated to MidoNet NSDB 
* Three (3) servers as MidoNet Gateways 

Physical Network: 

* One 1Gbps IP Network for NSDB 
* One 10Gbps IP Network for public network (if upstream links are 1Gbps, this could be 1Gbps) 
* One 10Gbps IP Network for Tunnel Zone 
* Public Classless Inter-Domain Routing (CIDR) block (Euca_public_IPs) 
* Three (3) BGP terminated uplinks, each of which coming from an independent router 
* ZooKeeper performance recommendations: 

Limits: 

* 500 to 600 MidoNet agents 
* Three (3) MidoNet Gateways 
* Tolerate 1 to 2 NSDB server failures 
* Tolerate 1 to 2 MidoNet Gateway/uplink failures 

**Deployment Topology** 

* A 5-node cluster for NSDB (co-located ZooKeeper and Cassandra) 
* eucanetd co-located with MidoNet API Server 
* Three (3) MidoNet Gateway Nodes 
* Hypervisors with Midolman 
* One 1Gbps IP network handling NSDB traffic 
* One 10Gbps IP network handling Tunnel Zone traffic 
* One 10Gbps IP network handling Public Network traffic 
* API communication via loopback/localhost network 

![image]({{< ref "/" >}}images/euca_mido_9v2.png)
*Figure 9: Production:Large deployment topology. A 1Gbps IP network carries NSDB; a 10Gbps IP network carries Tunnel Zone traffic; and another 10Gbps IP network carries Public Network traffic. A 5-node cluster for NSDB tolerates 2 server failures, and 3 gateways enable network failover and load balancing/sharing. Servers are bound to MidoNet in a way similar to Production:Small.* 

**NSDB Data Replication** 

* NSDB is deployed in a cluster of 5 nodes 
* ZooKeeper and Cassandra both have built-in data replication 
* Up to 2 server failures tolerated 

**MidoNet Gateway Failover** 

* Three paths are available to and from MidoNet, and failover is handled by BGP 

**MidoNet Gateway Load Balancing/Sharing** 

* Load Balancing from MidoNet is implemented by MidoNet agents (Midolman): ports in a stateful port group with default routes out are used in a round-robin fashion. 
* The customer AS should handle multi path routing in order to support load sharing/balancing to MidoNet; for example, Equal Cost Multi Path (ECMP).
