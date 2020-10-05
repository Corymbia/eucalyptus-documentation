+++
title = "Remove an Image"
weight = 10
+++

When a new image is uploaded to Eucalyptus, Eucalyptus saves the bundle and the image manifest to a bucket in Walrus. This bucket is stored in the Walrus directory that is defined in the Eucalyptus property `walrusbackend.storageDir` . The default value for this property is `/var/lib/eucalyptus/bukkits` . 

When you register an image, Eucalyptus creates the actual image file. Both the image manifest and the bundle must remain intact to run as an instance. 

To delete an image fully, you must deregister the image and delete the bundle. To successfully remove an image and associated bundle files: 

Find the image you want to remove. 

    euca-describe-images 
    IMAGE   emi-E533392E    alpha/centos.5-3.x86-64.img.manifest.xml    965590394582
    available   public   i386    machine eki-345135C9    eri-C4F135BC  instance-store
    IMAGE   emi-623C38B0  alpha/ubuntu.9-04.x86-64.img.manifest.xml   965590394582 
    available   public   i386    machine eki-E6B13926    eri-94DB3AB9  instance-store

Note the image file name (for example, emi-623C38B0). Deregister the image. 

    euca-deregister emi-623C38B0
    IMAGE   emi-623C38B0

Delete the bundle. 

    euca-delete-bundle -b alpha -p ubuntu.9-04.x86-64.img


{{% notice note %}}
If you accidentally try to delete a bundle for a second time, you might see an error message: . This error only displays if you try to delete a bundle that no longer exists. 
{{% /notice %}}
When you have finished these steps, display all images to confirm that the image was removed. 

    euca-describe-images 
    IMAGE   emi-E533392E    alpha/centos.5-3.x86-64.img.manifest.xml    965590394582
    available   public   i386    machine eki-345135C9    eri-C4F135BC  instance-store

