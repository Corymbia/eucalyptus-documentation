+++
title = "VPCMIDO Gateway Configuration Parameters"
weight = 10
+++

This topic provides detailed configuration parameter information for Eucalyptus VPCMIDO network mode.

## VPCMIDO Gateway Configuration
The following table provides a list of VPCMIDO parameters. 


| Parameter | Description | Validation | 
|  :---- |  :---- |  :---- | 
| BgpAsn | (Optional) Global BGP configuration *BGP Autonomous System Number assigned (to be decided by administrator/installer) for this VPCMIDO deployment. Private ASN range should be used:16-bit: 64512 - 6553432-bit: 131072 - 4199999999 (RFC6996) | Private use blocks recommended, but owners of public ASNs can use public ASNs or other blocks if they wish.Valid range is 1 - 4294967295. | 
| Gateways | (The VPCMIDO gateway parameters are below.) | Per MidoNet/BGP limitation, a maximum of 6 MidoGateways can be used. | 
| Ip | Internal IP address of Mido Gateway (not to be confused with the IP address of the gateway interface used in external communications). Note: Replaces 4.3 GatewayHost parameter. | Must be a valid IP address.Must be a live IP address configured on the machine. | 
| ExternalDevice | Device name of Mido Gateway interface that is physically connected to the external network (i.e., has L2 connectivity to the infrastructure router or BGP peer). This interface is dedicated for MidoNet use (Mido Gateway Operating System should not have control of this device). Note: Replaces 4.3 GatewayInterface parameter. | Must be a valid network interface connected to the network where L2 communication with BgpPeerIp (or ExternalRouterIp) can be established. | 
| ExternalCidr | CIDR block used in the external routing. Note: Replaces 4.3 PublicNetworkCidr parameter. | Must be a valid CIDR block. | 
| ExternalIp | IP address to be configured on ExternalDevice by eucanetd. Its subnet is as specified in ExternalCidr (ExternalCidr must contain ExternalIp). Note: Replaces 4.3 GatewayIP parameter. | Must be a valid and unused IP address.Must be within ExternalCidr.Must not be a network or broadcast address. | 
| ExternalRouterIp | IP address of an external router (for static configuration). This is the router IP address used in default routes for traffic originating from MidoNet. Note: Partially replaces 4.3 PublicGatewayIp parameter. | Must be a valid and unused IP address.Must be within ExternalCidr.Must not be a network or broadcast address.Either ExternalRouterIp or BgpPeerIp is required. | 
| BgpPeerIp | (Optional) BGP configuration * IP address of a BGP peer. This is the IP address to where MidoNet router will attempt to establish a BGP session.Note: Partially replaces 4.3 PublicGatewayIp parameter. | Must be a valid and unused IP address.Must be within ExternalCidr.Must not be a network or broadcast address.Either ExternalRouterIp or BgpPeerIp is required. | 
| BgpPeerAsn | (Optional) BGP configuration * BGP peer ASN for this MidoGateway. | Valid range is 1 - 4294967295. | 
| BgpAdRoutes | (Optional) BGP configuration * A list of CIDR blocks delegated to this VPCMIDO deployment. VPCMIDO BGP will be configured to advertise these routes. public IPs must be within these CIDR blocks. The same list can be used for all MidoGateways. The advantage of having a separate list per MidoGateway is that it allows different MidoGateways to be responsible for different CIDR blocks. If the same list of CIDR blocks is used for all MidoGateways, MidoNet built-in load sharing/balancing mechanism is used. | Each entry must be a valid CIDR block. | 
| PublicIps | The public IP address ranges associated with VPCMIDO. | With BGP: Each public IP must be within one of the CIDR blocks in the union of all BgpAdRoutes entries.Must be a valid IP address range.Must not contain network or broadcast address of the CIDR blocks in the union of all BgpAdRoutes.Without BGP: On-premise infrastructure must route all PublicIps to one of the MidoGateways. | 

Gateways with BGP require *BgpPeerAsn* , *BgpAdRoutes* , and *BgpAsn* . If all gateways are static (no BGP), *BgpAsn* is optional. A gateway with BGP has *BgpPeerAsn* and *BgpAdRoutes* parameters; a static gateway does not.

