+++
title = "Configure Bridges"
weight = 10
+++

To configure a bridge on CentOS 7 or RHEL 7, you need to create a file with bridge configuration (for example, ifcfg-brX) and modify the file for the physical interface (for example, ifcfg-ethX). The following steps describe how to set up a bridge on both CentOS 7 and RHEL 7. We show examples for configuring bridge devices that either obtain IP addresses using DHCP or statically. 

Install the `bridge-utils` package. 
    yum install bridge-utils

Go to the */etc/sysconfig/network-scripts* directory: 
    cd /etc/sysconfig/network-scripts

Open the network script for the device you are adding to the bridge and add your bridge device to it. The edited file should look similar to the following: 
    DEVICE=eth0
    # change the hardware address to match the hardware address your NIC uses
    HWADDR=00:16:76:D6:C9:45
    ONBOOT=yes
    BRIDGE=br0
    NM_CONTROLLED=no


{{% notice note %}}
The device name may vary. See the . 
{{% /notice %}}


Create a new network script in the */etc/sysconfig/network-scripts* directory called *ifcfg-br0* or something similar. The br0 is the name of the bridge, but this can be anything as long as the name of the file is the same as the `DEVICE` parameter, and the name is specified correctly in the previously created physical interface configuration (ifcfg-ethX). 
{{% notice note %}}
Choose names and use them consistently for all NCs (both the file name and the in the file). 
{{% /notice %}}
If you are using DHCP, the configuration will look similar to: 
    DEVICE=br0
    TYPE=Bridge
    BOOTPROTO=dhcp
    ONBOOT=yes
    DELAY=0

If you are using a static IP address, the configuration will look similar to: 
    DEVICE=br0
    TYPE=Bridge
    BOOTPROTO=static
    IPADDR=static_IP_address
    NETMASK=netmask
    GATEWAY=gateway
    ONBOOT=yes

Enter the following command: 
    systemctl restart network.service

