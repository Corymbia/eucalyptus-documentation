+++
title = "Create an Image from an Existing Instance-Store Instance"
weight = 10
+++

A common way to create a new image is to customize an existing instance.This example shows how to create a new instance store Eucalyptus image based on an existing instance store Eucalyptus instance. This topic describes how to create a new image by modifying an existing instance-store instance. 

Log on to an existing Eucalyptus instance-store instance and customize the instance. See Prepare a Linux Image for Eucalyptus []() for instructions on required changes the instance needs before re-bundling. Create a new image based on the image you just modified by using the `euca-bundle-instance` command, specifying a name, a description, and the instance ID of the Eucalyptus instance you customized in the previous step. For example: 
    euca-bundle-instance -b mybundle -p mycentos6 -o $EC2_ACCESS_KEY -w $EC2_SECRET_KEY i-96154365
    BUNDLE     bun-96154365     i-96154365     mybundle     mycentos     62013-11-05T21:37:23.469Z2013-11-05T21:37:23.469Z     pending     0

This command will the bundle task ID and exit immediately. In the background, Eucalyptus will begin the bundling process. Depending on the size of the instance, it can take several minutes for the bundling task to complete. 

You can monitor the status of the bundle task using the `euca-describe-bundle-tasks` command, supplying the ID of the image returned from the `eucalyptus-bundle-instance` command. For example: 


    euca-describe-bundle-tasks
    BUNDLE     bun-96154365     i-96154365     mybundle     mycentos6     2013-11-05T21:37:23.469Z2013-11-05T21:37:58.446Z     storing     0



Once the bundle task is complete, you can register thebundle as an instance-store image using the euca-register command, specifying the path to the bundle manifest in the format `[bucket]/[prefix].manifest.xml` . 
{{% notice note %}}
You should always explicitly declare the instance type of a bundle created with as an HVM type using --virtualization-type parameter. For example: 
{{% /notice %}}
`euca-register --virtualization-type=hvm mybundle/mycentos6.manifest.xml.` Your new image is now ready for use in your Eucalyptus cloud. 