+++
title = "Add a Windows Image to Eucalyptus"
weight = 10
hidden = true
+++

After the Windows virtual machine has been shut down, its entire disk can be uploaded to Eucalyptus as an HVM image. 

Extract the disk from the hypervisor into a file. With KVM, the disk may already be a file in raw format. If it's a file in a different format, convert it into raw disk format. If it's a block device, you can use 'dd' utility to copy contents of the block device into a file. Upload the raw disk file using the instructions in the [Install an HVM image](../image-guide/img_task_install_hvm_image.dita) section. 