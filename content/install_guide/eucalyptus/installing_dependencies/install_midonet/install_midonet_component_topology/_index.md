+++
title = "MidoNet Component Topology"
weight = 20
+++

This topic lists topology recommendations for installing MidoNet.

{{% notice note %}}
See [Understanding VPCMIDO and MidoNet]{{< ref preparing_vpc_midonet.md >}} for more information on MidoNet.
{{% /notice %}}

* The midonet-api must run co-located with the Cloud Controller (CLC). 
* Each Node Controller (NC) must run a Midolman agent. 
* The Cloud Controller (CLC) must run a Midolman agent. 
* It is recommended that your User Facing Services (UFS) host be used as the MidoNet Gateway (i.e., running a Midolman agent) when configuring . 
* The network interface(s) specified as * (in the configuration file) should be dedicated for /MidoNet (for configuration/operation/use). 
* /MidoNet expects exclusive use of the network interface specified in . 
* If the main network interface of a server is specified in , most likely the connectivity to that server will be lost once is deployed. 

## Network YAML Example

{{% notice note %}}
The older (JSON) network configuration format is still accepted, however the YAML format is recommended.
{{% /notice %}}

The following Eucalyptus network YAML file shows a sample VPCMIDO mode configuration:

    Mode: VPCMIDO
    
    InstanceDnsServers:
    - "10.10.10.1"
    
    PublicIps:
    - "1.A.B.1-1.A.B.255"
    
    Mido:
      Gateways:
      - ExternalCidr: "172.19.0.0/30"
        ExternalDevice: "veth1"
        ExternalIp: "172.19.0.2"
        ExternalRouterIp: "172.19.0.1"
        Ip: "10.10.10.1"

Where `1.A.B.1-1.A.B.255` represents the public IP address range for your cloud.
