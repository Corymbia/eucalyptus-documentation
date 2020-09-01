+++
title = "Create an EBS EMI"
weight = 5
+++

..  _concept_1tk_hdj_jf:

To create a new EMI that is used to boot EBS-backed instances: 

* Create a new volume whose size matches the size of the bootable file: 

* Attach the volume to a helper instance: 

* Log in to the instance and copy the bootable image from its source to the helper instance. 



* While logged in to the helper instance, copy a bootable image to the attached volume: 

* While logged in to the helper instance, flush the file system buffers after running the command: 

* Detach the volume from the instance: 

* Create a snapshot of the bootable volume: 

* Register the bootable volume as a new EMI: 

* Run a new EBS-backed instance: 



{{% notice note %}}The snapshot cannot be deleted unless the EMI is first deregistered. {{% /notice %}}

