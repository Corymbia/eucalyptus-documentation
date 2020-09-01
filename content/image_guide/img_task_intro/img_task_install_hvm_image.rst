+++
title = "Install an HVM Image"
weight = 5
+++

..  _img_task_install_hvm_image:

HVM (Hardware-assisted Virtual Machine) images are sequences of raw sectors of a complete bootable disk, including a boot loader and one or more partitions with an operating system. Such images are self-contained and can be booted on hardware that supports virtualization or on a full software emulation of hardware (QEMU). 

At run time, HVM images can be deployed to disks local to the hypervisor (so-called Instance Store images) or they can run off of dynamic volumes on EBS (so-called EBS-backed instances or boot-from-EBS instances). This topic covers methods for installing an HVM image into either type of EMI. 



=============================================
Install an HVM image as an Instance Store EMI
=============================================

Bundle, upload, and register the HVM image. All of this can be accomplished with a single command. For Linux images, the required options are: 

``euca-install-image -i /path/to/hvm-image -n name-of-the-image -r x86_64 --virtualization-type hvm -b bucket-name-for-image`` When installing a Windows image, an additional flag is necessary: 

``euca-install-image -i /path/to/hvm-image -n name-of-the-image -r x86_64 --virtualization-type hvm -b bucket-name-for-image --platform=windows`` 

=========================================
Install an HVM image as an EBS-Backed EMI
=========================================

An EBS-backed image (sometimes referred to as a "bfEBS" image) is an image with a root device that is an EBS volume created from an EBS snapshot. An EBS-backed image has a number of advantages (over an Instance Store image), including: 



* Faster boot time 

* Larger volume size limits 

* Changes to the data on the image persist after instance termination 



===================================================
Option A: Install an EBS image with euca-import-vol
===================================================

With this method, a single command uploads image data into Object Store and triggers a conversion task, which copies the data into an EBS volume. The volume will be the source of the snapshot behind the EBS-backed EMI.Import the HVM image file into Object Storage and then copy it into EBS. For example: ``euca-import-volume /path/to/hvm-image --format raw --availability-zone AZ-NAME --bucket bucket-for-hvm-image --owner-akid $EC2_ACCESS_KEY --owner-sak $EC2_SECRET_KEY --prefix image-name-prefix --description "textual description"`` {{% notice note %}}If the volume import process was interrupted, import can be resumed (within a one-week deadline) with the following command: 

{{% /notice %}}After the volume data has been uploaded to Object Store, an internal conversion task will copy the data into a new EBS volume. You can query the progress of this task with the following command: ``euca-describe-conversion-tasks import-vol-fae1e94d`` Once the task has finished successfully and the volume is available, you can take a snapshot of the volume: ``euca-create-snapshot <volume-id>`` You can now register the snapshot: ``euca-register --name <image-name> --snapshot <snapshot-id> --root-device-name <device>`` You've now created a EBS-backed image. To maintain data persistence, be sure to use ``euca-stop-instances`` and ``euca-start-instances`` to stop and start your EBS-backed instance. 

========================================================
Option B: Install an EBS image with euca-import-instance
========================================================

With this method, a single command uploads image data into the Object Store and triggers a conversion task; this conversion task copies the data into an EBS volumetakes a snapshot of the volume, registers the snapshot as an EMI, and deploys the EMI as an instance.Turn an HVM image into a running EBS instance with a single command: {{% notice note %}}Just as with euca-run-instance, one can specify the Instance Type for the instance that will run, as well as the SSH key. For example: {{% /notice %}}``euca-import-instance /root/paravirtualimage/ubuntuJune06.img --format raw --architecture x86_64 --platform Linux --availability-zone EDU --bucket import_instance --owner-akid $EC2_ACCESS_KEY --owner-sak $EC2_SECRET_KEY --prefix eduii --description "import instance" --key admin --instance-type m1.small`` {{% notice note %}}If volume import process was interrupted (by an interruption of the command or due to a network mishap, import can be resumed (within a one-week deadline). 

``euca-resume-import -t import-i-b393f3f6 /path/to/hvm-image`` 

{{% /notice %}}After the volume data has been uploaded to Object Store, an internal conversion task will copy the data into a new EBS volume. You can query the progress of this task with the following command: ``euca-describe-conversion-tasks import-i-b393f3f6`` Once the conversion task has finished successfully, you should see a running instance. You may log into that instance if you specified an SSH key. To maintain data persistence, be sure to use ``euca-stop-instances`` and ``euca-start-instances`` to stop and start your EBS-backed instance. 

======================================================
Option C: Install an EBS image using a helper instance
======================================================

This is a more manual method for installing an HVM image into an EBS-backed EMI. Instead of importing the image data into an EBS volume directly, a helper instance is used to copy data from the image file into the volume. The helper instance can be either an instance store or an EBS-backed instance, and can be deleted when ﬁnished. The volume will be the source of the snapshot behind the EBS-backed EMI.Create and launch a help instance. Create a volume big enough to hold the bootable image file: ``euca-create-volume -z <cluster_name> -s <size_in_GB>`` Attach the volume to the helper instance: ``euca-attach-volume <volume-id> -i <instance-id> -d <device>`` Log in to the instance and copy the bootable image to the attached volume by performing one of the following steps: If the bootable image is saved in an http or ftp repository, use ``curl`` or ``wget`` to download the .img file to the attached volume. For example: ``curl <path_to_bootable_image> > <device>`` 

If the bootable image is from a source other than an http or FTP repository, copy the bootable image from its source to the helper instance, and then copy it to the attached volume using the ``dd`` command. For example: ``dd if=<path_to_bootable_image> of=<device> bs=1M`` 

Detach the volume from the instance: ``euca-detach-volume <volume-id>`` Create a snapshot of the volume: ``euca-create-snapshot <volume-id>`` Register the snapshot: ``euca-register --name <image-name> --snapshot <snapshot-id> --root-device-name <device>`` You've now created a EBS-backed image. To maintain data persistence, be sure to use ``euca-stop-instances`` and ``euca-start-instances`` to stop and start your EBS-backed instance. 