+++
title = "Configure VPCMIDO Network Mode"
weight = 20
chapter = true
+++


# Configure VPCMIDO Network Mode
This topic provides configuration instructions for Eucalyptus VPCMIDO network mode. Eucalyptus requires network connectivity between its clients (end-users) and the cloud components (e.g., CC, CLC, and storage).
{{% notice note %}}
If you are not using VPCMIDO mode with , you can skip this topic. See . 
{{% /notice %}}


To configure VPCMIDO mode parameters, you must create a `network.json` configuration file. Later in the installation process you will []({{< ref nw_json_upload.md >}}) to the CLC. 

Create the network JSON file. Open a text editor. Create a file similar to the following structure. This example demonstrates two gateways and two BGP peers (sections relevant to VPCMIDO are shown here). Useful to ensure JSON is valid: http://jsonparseronline.com/ 

    {
        "Mido": {
            "BgpAsn": "64512",
            "Gateways": [
                {
                    "Ip": "10.111.5.11",
                    "ExternalDevice": "em1.116",
                    "ExternalCidr": "10.116.128.0/17",
                    "ExternalIp": "10.116.133.11",
                    "BgpPeerIp": "10.116.133.173",
                    "BgpPeerAsn": "65000",
                    "BgpAdRoutes": [
                        "10.116.150.0/24"
                    ]
                },
                {
                    "Ip": "10.111.5.22",
                    "ExternalDevice": "em1.117",
                    "ExternalCidr": "10.117.128.0/17",
                    "ExternalIp": "10.117.133.22",
                    "BgpPeerIp": "10.117.133.173",
                    "BgpPeerAsn": "65001",
                    "BgpAdRoutes": [
                        "10.117.150.0/24"
                    ]
                }
            ],
            "Mode": "VPCMIDO",
            "PublicIps": [
                "10.116.150.10-10.116.150.254",
                "10.117.150.10-10.117.150.254"
            ]
        }
    }

Save the `network.json` file. The following example demonstrates a gateway with static routing configuration. This configuration might be used for a Proof of Concept (POC) environment; however, it is not recommended for production. 



    {
        "Mido": {
            "Gateways": [
                {
                    "Ip": "10.111.5.11",
                    "ExternalDevice": "em1.116",
                    "ExternalCidr": "10.116.128.0/17",
                    "ExternalIp": "10.116.133.11",
                    "ExternalRouterIp": "10.116.133.173"
                }
            ]
        },
        "Mode": "VPCMIDO",
        "PublicIps": [
            "10.116.150.10-10.116.150.254"
        ]
    }



{{% children %}}
