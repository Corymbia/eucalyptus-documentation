+++
title = "Comparing Instance Types"
weight = 10
+++

The graphic below illustrates the differences between an instance store-backed instance and an EBS-backed instance.   Both types of instances still boot from an EMI; the difference is what is behind the EMI.   For an instance store-backed instance the EMI is backed by a bundled image.  For an EBS-backed instance the EMI is backed by a snapshot of a volume that contains bootable software, similar to a physical host's boot disk. 




![image]({{< ref "/" >}}images/Comparing-Types.png)




Note that for the instance store-backed instance, the EMI, EKI, and ERI (assuming Linux) are copied from the Walrus directly to Node Controller.  Both disk and memory on the Node Controller are used as cache so an instance store-backed instance can be considered a cache-based instance and is not persistent.  Once the instance is terminated both the RAM and the disk cache are cleared and any modifications to the instance are lost. 

When an EBS-backed instance is launched, the snapshot on which the EMI is based is automatically copied to a new volume which is then attached to the instance. The instance then boots from the attached volume. Changes to the EBS-backed instance are persistent because the volume used to boot the EBS-backed instance is persistent.  As a result, EBS-backed instances can be suspended and resumed and not just terminated like an instance store-backed instance. 



