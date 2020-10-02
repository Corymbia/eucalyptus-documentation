+++
title = "Configure EDGE Network Mode"
weight = 5
+++

This topic provides configuration instructions for Eucalyptus EDGE network mode. Eucalyptus requires network connectivity between its clients (end-users) and the cloud components (e.g., CC, CLC, and Walrus).
{{% notice note %}}
If you are not using EDGE mode with , you can skip this topic. See . 
{{% /notice %}}


To configure Eucalyptus for EDGE mode, most networking configuration is handled through settings in a global Cloud Controller (CLC) property file. 

The */etc/eucalyptus/eucalyptus.conf* file contains some network-related options in the “Networking Configuration” section. These options use the prefix VNET_. The most commonly used VNET options are described in the following table. 

The most commonly used VNET options are described in the following table. 


| Option | Description | Component | 
|  :---- |  :---- |  :---- | 
| VNET_BRIDGE | This is the name of the bridge interface to which instances' network interfaces should attach. A physical interface that can reach the CC must be attached to this bridge. Common setting for KVM is br0. | Node Controller | 
| VNET_DHCPDAEMON | The ISC DHCP executable to use. This is set to a distro-dependent value by packaging. The internal default is /usr/sbin/dhcpd3. | Node Controller | 
| VNET_MODE | The networking mode in which to run. The same mode must be specified on all CCs and NCs in your cloud. Valid values: EDGE | All CCs and NCs | 
| VNET_PRIVINTERFACE | The name of the network interface that is on the same network as the NCs. Default: eth0 | Node Controller | 
| VNET_PUBINTERFACE | This is the name of the network interface that is connected to the same network as the CC. Depending on the hypervisor's configuration this may be a bridge or a physical interface that is attached to the bridge. Default: eth0 | Node Controller | 

You must edit `eucalyptus.conf` on the Cluster Controller (CC) and Node Controller (NC) hosts. You must also create a JSON file and upload it the Cloud Controller (CLC). 


## CC Configuration
Log in to the CC and open the */etc/eucalyptus/eucalyptus.conf* file. Go to the **Network Configuration** section, uncomment and set the following: 
    VNET_MODE="EDGE"

Save the file. Repeat on each CC in your cloud. 
## NC Configuration
Log into an NC machine and open the */etc/eucalyptus/eucalyptus.conf* file. Go to the **Network Configuration** section, uncomment and set the following parameters: 
    VNET_MODE
    VNET_PRIVINTERFACE
    VNET_PUBINTERFACE"
    VNET_BRIDGE
    VNET_DHCPDAEMON

For example: 


    VNET_MODE="EDGE"
    VNET_PRIVINTERFACE="br0"
    VNET_PUBINTERFACE="br0"
    VNET_BRIDGE="br0"
    VNET_DHCPDAEMON="/usr/sbin/dhcpd"

Save the file. Repeat on each NC. 
## JSON Configuration
To configure the rest of the EDGE mode parameters, you must create a `network.json` configuration file. Later in the installation process you will [](nw_json_upload.dita#nw_edge_json_upload) to the CLC. 

Create the network JSON file. Open a text editor. Create a file similar to the following structure. Substitute comments for your system settings. See examples at the end of this topic. Useful to ensure JSON is valid: http://jsonparseronline.com/ 
    {
      "InstanceDnsDomain": ""
        "_comment": "Internal DNS domain used for instance private DNS names"
      "InstanceDnsServers": [],
        "_comment": "A list of servers that instances receive to resolve 
                     DNS names"
      "PublicIps": [],
        "_comment": "List of public IP addresses"
      "Subnets":   [],
        "_comment": "Subnets you want Eucalyptus to route through the private 
                     network rather than the public"
      "MacPrefix": "",
             "_comment": "First 2 octets of any VM's mac address launched"
      "Clusters":  [
        "_comment": "A list of cluster objects that define each 
                     availability zone (AZ) in your cloud"
        {
           "Name": "",
             "_comment": "Name of the cluster as it was registered"
           
           "Subnet": { 
             "_comment": "Subnet definition that this cluster will use for 
                          private addressing"
             "Name": "",
               "_comment": "Arbitrary name for the subnet"
             "Subnet": "",
               "_comment": "The subnet that will be used for private 
                            addressing"
             "Netmask": "",
               "_comment": "Netmask for the subnet defined above"
             "Gateway": "",
               _comment": "Gateway that will route packets for the 
                           private subnet"
           },
           "PrivateIps": []
             "_comment": "Private IPs that will be handed out to instances 
                          as they launch"
         },
      ]
    }

Save the `network.json` file. The following example is for a setup with one cluster (AZ), called PARTI00, with a flat network topology. 


    {
        "InstanceDnsDomain": "eucalyptus.internal",
        "InstanceDnsServers": ["10.1.1.254"],
        "MacPrefix": "d0:0d",
        "PublicIps": [
            "10.111.101.84",
            "10.111.101.91",
            "10.111.101.92",
            "10.111.101.93"
        ],
        "Subnets": [
        ],
        "Clusters": [
            {
                "Name": "PARTI00",
                "Subnet": {
                    "Name": "10.111.0.0",
                    "Subnet": "10.111.0.0",
                    "Netmask": "255.255.0.0",
                    "Gateway": "10.111.0.1"
                },
                "PrivateIps": [
                    "10.111.101.94",
                    "10.111.101.95"
                ]
            }
        ]
    }

For a multi-cluster deployment, add an additional cluster to your configuration for each cluster you have. The following example has an two clusters, PARTI00 and PARTI01. 


    {
        "InstanceDnsDomain": "eucalyptus.internal",
        "InstanceDnsServers": ["10.1.1.254"],
        "PublicIps": [
            "10.111.101.84",
            "10.111.101.91",
            "10.111.101.92",
            "10.111.101.93"
        ],
        "Subnets": [
        ],
        "Clusters": [
            {
                "Name": "PARTI00",
                "MacPrefix": "d0:0d",
                "Subnet": {
                    "Name": "10.111.0.0",
                    "Subnet": "10.111.0.0",
                    "Netmask": "255.255.0.0",
                    "Gateway": "10.111.0.1"
                },
                "PrivateIps": [
                    "10.111.101.94",
                    "10.111.101.95"
                ]
            },
            {
                "Name": "PARTI01",
                "MacPrefix": "d0:0d",
                "Subnet": {
                    "Name": "10.111.0.0",
                    "Subnet": "10.111.0.0",
                    "Netmask": "255.255.0.0",
                    "Gateway": "10.111.0.1"
                },
                "PrivateIps": [
                    "10.111.101.96",
                    "10.111.101.97"
                ]
            }
        ]
    }

