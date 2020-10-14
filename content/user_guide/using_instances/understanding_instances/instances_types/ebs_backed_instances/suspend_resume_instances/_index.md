+++
title = "Suspending and Resuming EBS-Backed Instances"
weight = 30
+++

An EBS-backed instance can be suspended and resumed, similar to the operating system and applications on a laptop.   The current state of the EBS-backed instance is saved in a suspend operation and restored in a resume operation.  Like instance store-backed instances, an EBS-backed instance can also be rebooted and terminated. 

To suspend a running EBS-backed instance: 

    euca-stop-instances i-<nnnnnnnn>

To resume a suspended EBS-backed instance: 

    euca-start-instances i-<nnnnnnnn>

To reboot an EBS-backed instance: 

    euca-reboot-instances i-<nnnnnnnn>

To terminate an EBS-backed instance: 

    euca-terminate-instances i-<nnnnnnnn>

