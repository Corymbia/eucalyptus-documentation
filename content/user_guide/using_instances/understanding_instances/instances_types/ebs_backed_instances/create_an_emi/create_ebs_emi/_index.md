+++
title = "Create an EBS EMI"
weight = 5
+++

To create a new EMI that is used to boot EBS-backed instances: 

1. Create a new volume whose size matches the size of the bootable file: 
1. Attach the volume to a helper instance: 
1. Log in to the instance and copy the bootable image from its source to the helper instance. 


1. While logged in to the helper instance, copy a bootable image to the attached volume: 
1. While logged in to the helper instance, flush the file system buffers after running the command: 
1. Detach the volume from the instance: 
1. Create a snapshot of the bootable volume: 
1. Register the bootable volume as a new EMI: 
1. Run a new EBS-backed instance: 



{{% notice note %}}
The snapshot cannot be deleted unless the EMI is first deregistered. 
{{% /notice %}}


