+++
title = "Monitoring"
weight = 70
+++

This topic includes details about which resources you should monitor.

| Component | Running Processes | 
|  :---- |  :---- | 
| Cloud Controller (CLC) | eucalyptus-cloud, postgres, eucanetd (VPCMIDO mode) | 
| User-facing services (UFS) | eucalyptus-cloud | 
| Walrus | eucalyptus-cloud | 
| Cluster Controller (CC) | eucalyptus-cluster | 
| Storage Controller (SC) | eucalyptus-sc, tgtd (for DAS and Overlay) | 
| Node Controller (NC) | eucalyptus-node, httpd, dhcpd, eucanetd (EDGE mode), qemu-kvm / 1 per instance | 
| Management Console | eucaconsole | 

