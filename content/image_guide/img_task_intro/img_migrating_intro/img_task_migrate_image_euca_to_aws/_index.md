+++
title = "Migrate a Linux Image from Eucalyptus to AWS"
weight = 10
hidden = true
+++

This topic describes how to migrate an image from Eucalyptus to AWS.
{{% notice note %}}
These are high-level guidelines for moving an instance from Eucalyptus to AWS. Specific examples will vary depending on the distro running on the image. 
{{% /notice %}}
Run an instance from the image you chose. 
    euca-run-instance emi-1A6338AE

SSH into the instance and verify that the instance is valid for use with AWS: Download the latest ec2-modules from [](http://s3.amazonaws.com/ec2-downloads) and put them into the `/lib/modules` directory on the instance. Copy the AWS EC2 certificate and private key from the AWS instance to your local workstation. Shut down unneeded services on the AWS instance (for example, Apache and MySQL). Clear out log files and bash history files. Remove your ssh keys from the instance. Reset passwords for the instance, and for any services that maintain their own password database. Clear out any temporary directories. Install Euca2ools on the instance. 

Mount a volume that is at least 1.5 times as large as the entire instance. Bundle the running instance. 
    euca-bundle-instance 

Switch the Euca2ools configuration file to use Eucalyptus 
    default-region = euca-release

Upload the AWS bundled instance to Eucalyptus. 
    euca-upload-bundle -b bucket_name -m manifest_file

Test the new uploaded image. 
    euca-run-instance emi-a6e15bcf

