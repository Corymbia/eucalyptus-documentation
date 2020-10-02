+++
title = "Networking Configuration Options"
weight = 10
+++

All network-related options specified in /etc/eucalyptus/eucalyptus.conf use the prefix VNET_. The most commonly used VNET options are described in the following table. 


{{% notice note %}}
If you change the value of in the file, you must restart the Cluster Controller. 
{{% /notice %}}


| Option | Description | Component | 
|  :---- |  :---- |  :---- | 
| VNET_BRIDGE | This is the name of the bridge interface to which instances' network interfaces should attach. A physical interface that can reach the CC must be attached to this bridge. Common setting for KVM is br0. | Node Controller | 
| VNET_DHCPDAEMON | The ISC DHCP executable to use. This is set to a distro-dependent value by packaging. The internal default is /usr/sbin/dhcpd3. | Node Controller | 
| VNET_MODE | The networking mode in which to run. The same mode must be specified on all CCs and NCs in your cloud. Valid values: EDGE | All CCs and NCs | 
| VNET_PRIVINTERFACE | The name of the network interface that is on the same network as the NCs. Default: eth0 | Node Controller | 
| VNET_PUBINTERFACE | This is the name of the network interface that is connected to the same network as the CC. Depending on the hypervisor's configuration this may be a bridge or a physical interface that is attached to the bridge. Default: eth0 | Node Controller | 

