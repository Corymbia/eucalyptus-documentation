+++
title = "Create an Image from an Existing EBS-Backed Instance"
weight = 10
+++

A common way to create a new image is to customize an existing instance. This topic describes how to create a new image by modifying an existing EBS-backed instance.This example shows how to create a new EBS-backed Eucalyptus image based on an existing EBS-backed Eucalyptus instance. 

Log on to an existing Eucalyptus EBS-backed instance and customize the instance. Prepare the image. See []() for instructions. Create a new image based on the image you just modified by using the eucalyptus-create-image command, specifying a name, a description, and the instance ID of the Eucalyptus instance you customized in the previous step. For example: `euca-create-image -n "mynewimage" -d "This is my new custom recycled image" i-1ABCDEFF` This command will show the ID of the new machine image and exit immediately. In the background, Eucalyptus will begin the process of creating a new image based on the instance you supplied. 

You can monitor the status of the image using the euca-describe-images command, supplying the ID of the image returned from the euca-create-image command. For example: 

`euca-describe-images i-e12398ab` 