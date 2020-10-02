+++
title = "Image Overview"
weight = 5
+++

An image defines what will run on a guest instance in your Eucalyptus cloud. An image contains everything necessary to boot and run an operating system: either one of the Linux distributions – CentOS, Fedora, Ubuntu, Debian, etc – or one of the supported Windows server versions.Images of two types are supported by Eucalyptus: 

* are raw disks that can boot independently. They can contain Linux or Windows operating systems. HVM stands for Hardware-assisted Virtual Machine because such images can only run efficiently on hardware that supports virtualization. When an HVM image is uploaded and registered, it becomes a Eucalyptus Machine Image (EMI) of type "hvm", with a unique ID. 
* are Linux images that can boot if they are paired with a kernel and ramdisk that are compatible with the host's hypervisor. Currently only root file system images are supported (on AWS, a paravirtual image can be a file system or a full disk). When a paravirtual image is uploaded and registered, it also becomes an EMI of "paravirtual" type, which needs to be paired with a kernel (EKI) and ramdisk (ERI) images to be usable. EKI contains a kernel (i.e., the ‘vmlinuz’ file typically found in the /boot directory of a Linux system). ERI contains the kernel modules (i.e., the ‘initrd’ file from the /boot directory). 


Depending on the method used for upload, an instance's disk will reside on one of two types of storage: 

* volumes are located on temporary disk space that is destroyed when instances shut down. These volumes are based on a template residing in Object Storage. Instance Store can host either HVM or paravirtual images. 
* volumes are disks with lifetimes that can be independent of instances. These volumes are based on snapshots of EBS volumes (instead of templates in Object Storage). Only HVM images can be deployed on EBS in Eucalyptus (in AWS, EBS can also host paravirtual images). 


To help get you started, Eucalyptus provides pre-packaged virtual machine images that are ready to run in your cloud. You can download them from the Eucalyptus Machine Image catalog . Both HVM and paravirtual images are available there. Each paravirtual image comes bundled with a corresponding EKI and ERI. 

If you find that the pre-packaged images don't meet your needs, you can migrate an image from another cloud system (such as Amazon Web Services) or create your own image. See the rest of this guide for more information. 


{{% notice note %}}
For a list of supported guest operating systems, . 
{{% /notice %}}
