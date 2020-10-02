+++
title = "Migrate a Linux Image from AWS to Eucalyptus"
weight = 10
+++

You can migrate an S3-backed image from AWS to Eucalyptus.
{{% notice note %}}
This topic assumes you are migrating an S3-backed Amazon Machine Image (AMI) that you own. For instructions on creating an S3-backed AMI from an existing AMI, see . 
{{% /notice %}}

{{% notice note %}}
Specific examples may vary depending on the distro running on the image that you want to migrate. 
{{% /notice %}}
Set up your Euca2ools configuration to work with both Eucalyptus and Amazon Web Services. Check ownership of the AMI that you want to migrate to Eucalyptus by using the euca-describe-images command. For example: 
    euca-describe-images --region us-east-1 --owner 999999999999
    IMAGE	ami-e1a1e888	999999999999/precise-test	999999999999	available	private		x86_64	machine	aki-88aa75e1			instance-store	paravirtual	xen
    	BLOCKDEVICEMAPPING	EPHEMERAL	sda2	ephemeral0

Run the AWS instance. 
    euca-run-instance ami-e1a1e888 --region us-east-1 

Install Euca2ools on the instance. For instructions, see the Euca2ools Guide. Make sure that you have enough space on a volume to hold the bundle that we will create. Bundle the running AWS instance. For example: 
    sudo -s
    ec2-bundle-vol -b testbucket -d /mnt -u 4299-4227-3585 -k my-aws.pem -c my-aws-cert.pem -r x86_64 -s 2048
    Copying / into the image file /mnt/image...
    Excluding:
    	 /dev/pts
    	 /
    	 /sys
    	 /proc
    	 /proc/sys/fs/binfmt_misc
    	 /dev
    	 /media
    	 /mnt
    	 /proc
    	 /sys
    	 /mnt/image
    	 /mnt/img-mnt
    1+0 records in
    1+0 records out
    1048576 bytes (1.0 MB) copied, 0.00209056 s, 502 MB/s
    mke2fs 1.42.3 (14-May-2012)
    Bundling image file...
    Splitting /mnt/image.tar.gz.enc...
    Created image.part.00
    Created image.part.01
    [example truncated]
    Created image.part.30
    Generating digests for each part...
    Digests generated.
    Unable to read instance meta-data for ancestor-ami-ids
    Unable to read instance meta-data for ramdisk-id
    Unable to read instance meta-data for product-codes
    Creating bundle manifest...
    ec2-bundle-vol complete.

Switch the Euca2ools configuration file to use Eucalyptus. You can do this by specifying the Eucalyptus region as defined in your Euca2ools configuration file by specifying the `--region` parameter on the command line, or by changing the `default-region` option in the Euca2ools configuration file: 
    default-region = euca-release

Download the bundle from the AWS S3 bucket: 
    euca-download-bundle --bucket testbucket --directory /tmp/aws-image/ --region us-east-1

Unbundle the AWS instance bundle: 
    euca-unbundle --manifest /tmp/aws-image/image.manifest.xml --source /tmp/aws-image/ --destination /tmp/aws-image/ --region us-east-1

Run some checks to make sure that the image can be used with Eucalyptus: Mount the image via loopback: 
    #  sudo mkdir /mnt/aws-image
    	#  sudo mount -o loop /tmp/aws-image/image /mnt/aws-image
    	#  df -ah 
    	……
    	/tmp/aws-image/image
                          9.9G  1.1G  8.3G  12% /mnt/aws-image

Make sure that the distro repositories in the image do not point to EC2-specific repositories. TODO: Need an actual example here. Install a non-Xen kernel into the image from distro and make sure VirtIO modules are added. TODO: Need an actual example here. Extract the ramdisk and kernel to be bundled, uploaded and registered as ERI and EKI files. In this example, initrd.img-3.2.0-53-virtual and vmlinuz-3.2.0-53-virtual will be copied from /mnt/aws-image/boot to the /tmp/aws-image directory: 
    # sudo cp /mnt/aws-image/boot/initrd.img-3.2.0-53-virtual /tmp/aws-image/.
    # sudo cp /mnt/aws-image/boot/vmlinuz-3.2.0-53-virtual /tmp/aws-image/.

Make sure that the file system of the image is either ext2, ext3, or ext4 by using the file command. For example: 
    # file /tmp/aws-image/image
    /tmp/aws-image/image: Linux rev 1.0 ext4 filesystem data (extents) (large files) (huge files)

Bundle the image using euca-bundle-image: 
    euca-bundle-image -i /tmp/aws-image/image

Upload the AWS bundled instance to Eucalyptus. 
    euca-upload-bundle -b hybrid-guide-sample-bucket -m /tmp/aws-image/image.manifest.xml --access-key myaccesskey --secret-key mysecretkey

Test the new uploaded image. 
    euca-run-instance emi-a6e15bcf

