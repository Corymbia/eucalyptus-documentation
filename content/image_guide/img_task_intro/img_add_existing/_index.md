+++
title = "Install a paravirtual image"
weight = 50
chapter = true
+++


# Install a paravirtual image

{{% notice note %}}
As of Eucalyptus version 4.0, it is now required to pass a Eucalyptus Kernel Image (EKI) and a Eucalyptus Ramdisk Image (ERI) when uploading and registering a paravirtual Eucalyptus Machine Image (EMI) using the , , and command line tools. 
{{% /notice %}}

Once you've customized or acquired a paravirtual image to use with Eucalyptus, you can enable the image as an executable entity with the following steps: 

1. Unless a suitable kernel is already registered, bundle the kernel, upload it to Object Storage, and register it as a new EKI. 
1. Unless a suitable ramdisk is already registered, bundle the ramdisk, upload it to Object Storage, and register it as a new ERI 
1. Bundle the root disk image, which must be a Linux partition, requesting the kernel and ramdisk that you desire, upload the bundle to Object Storage, and register it as a new EMI. 

{{% notice note %}}
Note that while all users can bundle, upload and register images, only users under the account have the required permissions to upload and register kernels and ramdisks. 
{{% /notice %}}

Once you have an image that meets your needs, perform the tasks listed in this section to add the image to your cloud. 


{{% children sort="weight" %}}
