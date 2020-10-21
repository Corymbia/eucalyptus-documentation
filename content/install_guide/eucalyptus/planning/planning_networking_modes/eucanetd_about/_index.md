+++
title = "About Eucanetd"
weight = 10
+++

The eucanetd service implements artifacts to manage and define Eucalyptus cloud networking. Eucanetd runs alongside the CLC or NC services, depending on the configured networking mode. Eucanetd manages network functionality. For example: 

* Installs network artifacts (iptables, ipsets, ebtables, dhcpd) 
* Performs state management for the installed network artifacts 
* Updates network artifact configuration as needed 
* In VPCMIDO mode: 
  * Interacts with MidoNet via the MidoNet API
  * Defines network artifacts in MidoNet



## Where to deploy eucanetd
Deploy *eucanetd* depending on the selected network mode: 

| Host Machine | EDGE mode | VPCMIDO mode |
|  :---- |  :---- |  :---- |
| CLC | No | Yes |
| NC | Yes | No |

When required for a mode *eucanetd* should be deployed on all hosts for that service.
