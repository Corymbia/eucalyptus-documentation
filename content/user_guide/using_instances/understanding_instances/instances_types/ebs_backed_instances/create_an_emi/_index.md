+++
title = "EBS EMI Creation Overview"
weight = 5
chapter = true
+++


# EBS EMI Creation Overview
You can create an EBS EMI from an existing *.img* file or create your own *.img* file.  One way to create your own EBS *.img* file is to use `virt-install` as described below. 

Use `virt-install` on a system with the same operating system version and hypervisor as your Node Controller. When using `virt-install` , select *scsi* as the disk type for KVM if the VIRTIO paravirtualized devices are not enabled. If you have KVM with VIRTIO enabled (the default), select *virtio* as the disk type of the virtual machine. If you create, successfully boot, and connect the virtual machine to the network in this environment, it should boot as an EBS-backed instance in the Eucalyptus cloud. 


{{% notice note %}}
For CentOS or RHEL images, you will typically need to edit the file and remove the line. This is because an instance's network interface will always be assigned a different hardware address at instantiation. 
{{% /notice %}}



{{% notice note %}}
: If you use an image created by under a different distribution or hypervisor combination, it is likely that it will not install the correct drivers into the ramdisk and the image will not boot on your Node Controller. 
{{% /notice %}}


To create an EMI for EBS-backed instances will require initial assistance from a *helper* instance.  The helper instance can be either an instance store-backed or EBS-backed instance and can be deleted when finished.  It only exists to help create the initial volume that will be the source of the snapshot behind the EMI used to boot other EBS-backed instances. 

First you will need to create a volume large enough to contain the boot image file that was created by `virt-install` .  Once this volume has been created attach it to the helper instance. Then transfer the boot image file to the helper instance.  The helper instance must have enough free disk space to temporarily hold the boot image file. Once there, transfer the boot image file, using the `dd` command, to the attached volume. 

At this point the volume can be detached from the helper instance, a snapshot taken, and the snapshot registered as a new EMI. 

The process to create a new EMI is summarized as follows: 

1. Create the file using (the file is the virtual machine's disk file). 
1. Create the helper instance. 
1. Create and attach the volume to the helper instance. 
1. Copy the file to the helper instance and from there to the attached volume. 
1. Detach the volume and take a snapshot of it. 
1. Register the snapshot as a new EMI. 


This process is illustrated below. 




![image]({{< ref "/" >}}images/Creating-an-EBS-EMI.png)




{{% children %}}
