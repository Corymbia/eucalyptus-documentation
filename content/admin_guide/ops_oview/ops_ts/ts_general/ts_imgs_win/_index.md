+++
title = "Windows Images"
weight = 5
+++

This topic contains information to help you troubleshoot your Windows images.
## Properties
A typical size of Windows images is large and Eucalyptus has a set of properties that limit the size of various storage components. The first step in troubleshooting is to make sure that the values are large enough to store your Windows images. You can modify a property using 


    /usb/sbin/euctl-modify-property -p <property>=<value>

The properties that might affect registering Windows images are: 



* : max bucket size enforced by Walrus; should be larger than a Windows image 
* : if a Windows image is a type of EBS-backed EMI, this should be large enough to store all EBS backed images 
* : if a Windows image is a type of EBS-backed EMI, this should be large enough to store the image 
In addition, during the `euca-run-instances` , the CLC may time-out an instance while a large windows image (images in both Walrus and EBS) is being launched. We recommend that you raise the values of the following properties. 



* : maximum wait time, in minutes, before the instance becomes running. Am instance cannot stay in pending longer than this. Default: 60 
* : maximum wait time, in minutes, before a volume backing a boot from EBS image is created. Default: 30 

## Image Preparation

euca-bundle-image hangs
 The time to bundle an image is proportional to the image size. Because the typical size of Windows image is big, give enough time until bundling is complete. As a rule of thumb, it may take up to 20 min. for bundling a 10 GB Windows image. 
euca-upload-bundle fails
 Make sure `walrusbackend.storagemaxbucketsizeinmb` is large enough. If not, ask your administrator. 

## Instance Launch and Login

Instance stays in pending
 Typically, it takes longer to launch Windows images than Linux images as the delay is proportional to the image size. This can be especially long when the image is seeded on NCs the first time (images are cached in NCs and run within few seconds thereafter). As a rule of thumb, 10 GB Windows images may take up to 10 minutes to become ‘running’ when it is not cached in NCs. 
Instance stay in pending and goes to shutdown
 An instance may time-out if the Windows image is too big. Review and adjust the relevant properties. 
Instance is running, but not accessible using Remote Desktop.
 after instances become running, you should wait until Windows is fully booted. If the image is sysprepped, the booting time may take up to 10 min. Also you should make sure the followings are cleared: 

* The port 3389 is authorized in the security group 
* If the instance is attached to your active directory domain, the domain GPO shouldn’t block the RDP port (3389) 
* The username should be authorized to log-in using Remote Desktop (refer to User guide: Windows integration service) 

Finding the login username and password
 Use Administrator and the password retrieved by `euca-get-password` . If the instance is attached to a domain, you may use your domain username and password (make sure the username is prepended with domain name, such as *YOUR_DOMAIN\Alice* ). 
Can’t retrieve windows password using euca-get-password
 Make sure the platform field of your windows EMI is set to ‘windows’, not ‘linux’ (use `euca-describe-images` ). If not, the most likely reason is that the image name does not begin with ‘windows’. You should bundle/upload/register the image with a proper name. 
Instance is not attached to an Active Directory domain
 

* Make sure the parameters set in Windows integration service are correct. One way to verify them is to log in the instance using Administrator password and manually attach the instance to the domain (System Properties -> Computer Name) using the same parameters. 
* Make sure in eucalyptus.conf is set to the domain controller (refer to User Guide: Configure Active Directory). 


## Disk and Volume

Ephemeral disks are not visible in the Windows
 Open Disk Management console ( All Programs -> Administrative Tools -> Server Manager -> Storage ) and find the uninitialized disks. You should create a partition on the disk and format it. 
EBS volume is attached, but not visible in the Windows
 Open Disk Management console ( All Programs -> Administrative Tools -> Server Manager -> Storage ) and find the uninitialized disks. You should create a partition on the disk and format it. You don’t have to repeat it when the volume is reattached later. 
EBS volume is detached, but the disk drive (for example, E:\) is still visible in the Windows
 For KVM hypervisor, you should perform “remove hardware safely” before detaching the volume. 
euca-bundle-instance fails
 Make sure the bucket specified with ‘-b’ option doesn’t already exist and the property `walrusbackend.storagemaxbucketsizeinmb` is large enough to store the image. 
