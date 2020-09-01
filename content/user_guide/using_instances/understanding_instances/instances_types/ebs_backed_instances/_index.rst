+++
title = "EBS-Backed Instances"
weight = 5
chapter = true
+++

..  _concept_mjr_3fv_bh:



====================
EBS-Backed Instances
====================

Eucalyptus supports two different types of instances; instance store-backed instances and EBS-backed instances. This section describes EBS-backed instances. 

With EBS-backed instances you are booting an instance from a volume rather than a bundled EMI image. The boot volume is created from a snapshot of a root device volume. EBS-backed instances can be either Linux or Windows. The boot volume is persistent so changes to the instance are persistent. 

{{% notice note %}}Linux boot-from-EBS instances do not require EKI and ERI images like instance store-backed instances. {{% /notice %}}



.. image:: {{< ref "/" >}}images/EBS-Backed-Instances.png





