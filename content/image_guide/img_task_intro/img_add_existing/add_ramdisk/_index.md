+++
title = "Add a Ramdisk"
weight = 20
+++

When you add a ramdisk to Walrus, you bundle the ramdisk file, upload the file to a bucket in Walrus that you name, and then register the ramdisk with Eucalyptus. 

To add a ramdisk to Walrus: 

Use the following three commands: 

    euca-bundle-image -i <ramdisk_file> --ramdisk true -r x86_64
    euca-upload-bundle -b <ramdisk_bucket> -m /tmp/<ramdisk_file>.manifest.xml
    euca-register <ramdisk_bucket>/<ramdisk_file>.manifest.xml -n <name_of_ramdisk>

For example: 



    euca-bundle-image -i euca-fedora-10-x86_64/xen-kernel/initrd-2.6.27.21-0.1-xen 
    --ramdisk true -r x86_64
    ...
    Generating manifest /tmp/initrd-2.6.27.21-0.1-xen.manifest.xml
    
    euca-upload-bundle -b example_rd_bucket -m /tmp/initrd-2.6.27.21-0.1-xen.manifest.xml
    ...
    Uploaded image as example_rd_bucket/initrd-2.6.27.21-0.1-xen.manifest.xm
    
    euca-register example_rd_bucket/initrd-2.6.27.21-0.1-xen.manifest.xml -n mynewramdisk
    IMAGE	eri-XXXXXXXX 

Where the returned value `eri-XXXXXXXX` is the unique ID of the registered ramdisk image. 

