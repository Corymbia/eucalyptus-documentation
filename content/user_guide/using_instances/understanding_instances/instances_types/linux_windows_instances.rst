+++
title = "Linux and Windows Instances"
weight = 5
+++

..  _concept_zrn_ljw_df:

A Linux instance store-backed instance actually consists of three separate images: 

* The Linux boot disk image (EMI) as previously defined 

* A Eucalyptus kernel image (EKI), which is a low level operating system component that interfaces with the instance's virtual hardware 

* A Eucalyptus ramdisk image (ERI) - the initrd - which is the initial root file system that is loaded as part of the kernel boot procedure and loads modules that make it possible to access the real root file system in the second stage of the boot process 



When a Linux instance is launched, these three images (along with a few other files) are bound together using loop devices so that they appear as a single disk to the Linux operating system running in the instance. For Linux images, the same kernel and ramdisk files can be shared across multiple boot disk images, which allows for more efficient use of storage. 





.. image:: {{< ref "/" >}}images/Linux-Instance.png





A Windows instance store-backed instance consists only of the bootable file system image (EMI). The reason for this is that in the Windows operating system the kernel and ramdisk components cannot be separated from the boot disk image, and thus each copy of a Windows image must also contain a copy of these components. 





.. image:: {{< ref "/" >}}images/Windows-Instance.png



