+++
title = "Install and Configure the Imaging Service"
weight = 50
+++

The Eucalyptus Imaging Service, introduced in Eucalyptus 4.0, makes it easier to deploy EBS images in your Eucalyptus cloud and automates many of the labor-intensive processes required for uploading data into EBS images.

The Eucalyptus Imaging Service is implemented as a system-controlled "worker" virtual machine that is monitored and controlled via Auto Scaling. Once the Imaging Service is configured, the Imaging Service VM will be started automatically upon the first request that requires it: such as an EBS volume ingress. Specifically, in this release of Eucalyptus , these are the usage scenarios for the Eucalyptus Imaging Service: 

* **Importing a raw disk image as a volume:** If you have a raw disk image (containing either a data partition or a full operating system with a boot record, e.g., an HVM image), you can use the Imaging Service to import this into your cloud as a volume. This is accomplished with the `euca-import-volume` command. If the volume was populated with a bootable disk, that volume can be snapshotted and registered as an image. 
* **Importing a raw disk image as an instance:** If you have a raw disk image containing a bootable operating system, you can import this disk image into as an instance: the Imaging Service automatically creates a volume, registers the image, and launches an instance from the image. This is accomplished with the `euca-import-instance` command, which has options for specifying the instance type and the SSH key for the instance to use. 

## Install and Register the Imaging Worker Image
Eucalyptus provides a command-line tool for installing and registering the Imaging Worker image. Once you have run the tool, the Imaging Worker will be ready to use.Run the following commands on the machine where you installed the `eucalyptus-service-image` RPM package (it will set the `imaging.imaging_worker_emi` property to the newly created EMI of the imaging worker): 

    esi-install-image --region localhost --install-default

Consider setting the `imaging.imaging_worker_keyname` property to an SSH keyname (previously created with the `euca-create-keypair` command), so that you can perform troubleshooting inside the Imaging Worker instance, if necessary: 

    euctl services.imaging.worker.keyname=mykey


## Managing the Imaging Worker Instance
Eucalyptus automatically starts Imaging Worker instances when there are tasks for workers to perform.The cloud administrator can list the running Imaging Worker instances, if any, by running the command: 

    euca-describe-instances --filter tag-value=euca-internal-imaging-workers

To delete / stop the imaging worker: 

    esi-manage-stack -a delete imaging

To create / start the imaging worker: 

    esi-manage-stack -a create imaging

Consider setting the `imaging.imaging_worker_instance_type` property to an Instance Type with enough ephemeral disk to convert any of your paravirtual images. The Imaging Worker root filesystem takes up about 2GB, so the maximum paravirtual image that the Imaging Worker will be able to convert is the disk allocation of the Instance Type minus 2GBs. 

    euctl services.imaging.worker.instance_type=m3.xlarge


## Troubleshooting Imaging Worker
If the Imaging Worker is configured correctly, users will be able to import data into EBS volumes with `euca-import-*` commands, and paravirtual EMIs will run as instances. In some cases, though, paravirtual images may fail to convert (e.g., due to intermittent network failures or a network setup that doesn't allow the Imaging Worker to communicate with the CLC), leaving the images in a special state. To troubleshoot:If the Imaging Worker Instance Type does not provide sufficient disk space for converting all paravirtual images, the administrator may have to change the Instance Type used by the Imaging Worker. After changing the instance type, the Imaging Worker instance should be restarted by terminating the old Imaging Worker instance: 

    euctl services.imaging.worker.instance_type=m2.2xlarge
    euca-terminate-instances $(euca-describe-instances --filter tag-value=euca-internal-imaging-workers | grep INSTANCE | cut -f 2)

If the status of the conversion operation is 'Image conversion failed', but the image is marked as 'available' (in the output of euca-describe-images), the conversion can be retried by running the EMI again: 

    euca-run-instances ...

