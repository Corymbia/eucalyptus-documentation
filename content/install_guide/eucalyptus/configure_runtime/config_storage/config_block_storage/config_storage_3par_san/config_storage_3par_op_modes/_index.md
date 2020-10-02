+++
title = "About Operation Mode Optimization"
weight = 10
+++

This topic describes the operation modes available for 3PAR SAN backends for Eucalyptus cloud.The Eucalyptus 3PAR backend provider implements a mapping between EBS and 3PAR concepts. Operation mode optimization allows you to make storage operations more efficient in your cloud. Predominant use cases are described below. 


{{% notice note %}}
Operation modes are mutually exclusive and cannot be combined. Choose the strategy that is best for your 3PAR storage operations. The setting is at the SC level. 
{{% /notice %}}
Snapshot to volume optimization The default use case assumes that you snapshot rarely, create volumes from snapshots (without growing volumes) often, and you run EBS-backed instances often. 

Supporting this use case, the default `threeparoptimizesnaptovol` setting is `true` . 

Summary of operations: 

* EBS volumes and snapshots map to 3PAR virtual volumes 
* EBS snapshot from EBS volume translates to 3PAR copy operation 
* EBS volume from EBS snapshot translates to: 



![image]({{< ref "/" >}}images/3par_snaptovol_opt.png)
Volume to snapshot optimization This use case assumes that you snapshot often, but create volumes from snapshots rarely. 

If this use case is the best strategy for your storage operations, set `threeparoptimizesnaptovol` to `false` . 

Summary of operations: 

* EBS volumes and snapshots map to 3PAR virtual volumes 
* EBS snapshot from EBS volume translates to 3PAR copy operation 
* EBS volume from EBS snapshot translates to 3PAR physical copy operation 



![image]({{< ref "/" >}}images/3par_voltosnap_opt.png)
