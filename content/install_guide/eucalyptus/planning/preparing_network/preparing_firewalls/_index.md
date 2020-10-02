+++
title = "Reserve Ports"
weight = 5
+++


| Port | Description | 
|  :---- |  :---- | 
| TCP 5005 | DEBUG ONLY: This port is used for debugging (using the --debug flag). | 
| TCP 8772 | DEBUG ONLY: JMX port. This is disabled by default, and can be enabled with the --debug or --jmx options for CLOUD_OPTS. | 
| TCP 8773 | Web services port for the CLC, user-facing services (UFS), object storage gateway (OSG), Walrus SC; also used for external and internal communications by the CLC and Walrus. Configurable with euctl. | 
| TCP 8774 | Web services port on the CC. Configured in the eucalyptus.conf configuration file | 
| TCP 8775 | Web services port on the NC. Configured in the eucalyptus.conf configuration file. | 
| TCP 8777 | Database port on the CLC | 
| TCP 8779 (or next available port, up to TCP 8849) | jGroups failure detection port on CLC, UFS, OSG, Walrus SC. If port 8779 is available, it will be used, otherwise, the next port in the range will be attempted until an unused port is found. | 
| TCP 8888 | The default port for the Management Console. Configured in the /etc/eucalyptus-console/console.ini file. | 
| TCP 16514 | TLS port on Node Controller, required for instance migrations | 
| UDP 7500 | Port for diagnostic probing on CLC, UFS, OSG, Walrus SC | 
| UDP 8773 | Membership port for any UFS, OSG, Walrus, and SC | 
| UDP 8778 | The bind port used to establish multicast communication | 
| TCP/UDP 53 | DNS port on UFS | 
| UDP 63822 | eucanetd binds to localhost port 63822 and uses it to detect and avoid running multiple instances (of eucanetd) | 


{{% notice note %}}
For information about ports used by MidoNet, see the (Category OpenStack can be ignored). 
{{% /notice %}}


