+++
title = "Elastic Load Balancing"
weight = 10
+++

This topic explains suggestions for problems you might have with Elastic Load Balancing (ELB).
Can't synchronize with time server
 Eucalyptus sets up NTP automatically for any instance that has an internet connection to a public network. If an instance doesn't have such a connection, set the cloud property `loadbalancing.loadbalancer_vm_ntp_server` to a valid NTP server IP address. For example: 

    euctl loadbalancing.loadbalancer_vm_ntp_server=169.254.169.254
    PROPERTY	loadbalancing.loadbalancer_vm_ntp_server	169.254.169.254 was {}


Need to debug an ELB instance
 To debug an ELB instance, set the `loadbalancing.loadbalancer_vm_keyname` cloud property to the keypair of the instance you want to debug. For example: 

    # euctl loadbalancing.loadbalancer_vm_keyname=sshlogin
    PROPERTY	loadbalancing.loadbalancer_vm_keyname	sshlogin was {}


