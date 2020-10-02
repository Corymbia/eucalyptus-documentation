+++
title = "MidoNet Component Topology"
weight = 10
+++

This topic lists topology recommendations for installing Midokura Enterprise MidoNet.
{{% notice note %}}
See for more information on MidoNet. 
{{% /notice %}}


* The midonet-api must run co-located with the Cloud Controller (CLC). 
* Each Node Controller (NC) must run a Midolman agent. 
* The Cloud Controller (CLC) must run a Midolman agent. 
* It is recommended that your User Facing Services (UFS) host be used as the MidoNet Gateway (i.e., running a Midolman agent) when configuring . 
* The network interface(s) specified as * (in the configuration file) should be dedicated for /MidoNet (for configuration/operation/use). 
* /MidoNet expects exclusive use of the network interface specified in . 
* If the main network interface of a server is specified in , most likely the connectivity to that server will be lost once is deployed. 
* In Eucalyptus 4.4, `ExternalDevice` replaces `GatewayInterface` in 4.3 and prior releases. 


## 4.3 Network JSON Example

{{% notice note %}}
This 4.3 version of the VPCMIDO file is still accepted, however we strongly encourage use of the updated 4.4 template instead. See . 
{{% /notice %}}
The following Eucalyptus 4.3 network JSON template file shows a sample VPCMIDO mode configuration: 

Useful to ensure JSON is valid: http://jsonparseronline.com/ 
    
    {
      "InstanceDnsServers": [
        "UFS_HOST"
      ],
      "Mido": {
        "EucanetdHost": "clcfrontend",
        "GatewayHost": "ufsfrontend",
        "GatewayIP": "172.19.0.2",
        "GatewayInterface": "veth1",
        "PublicGatewayIP": "172.19.0.1",
        "PublicNetworkCidr": "172.19.0.0/30"
      },
      "Mode": "VPCMIDO",
      "PublicIps": [
        "PUBLIC_IPS"
      ]
    }

