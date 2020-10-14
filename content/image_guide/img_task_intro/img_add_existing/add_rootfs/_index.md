+++
title = "Add a Root Filesystem"
weight = 30
+++

When you add a root filesystem to Walrus, you bundle the root filesystem file, upload the file to a bucket in Walrus that you name, and then register the root filesystem with Eucalyptus. The bundle operation can include a registered ramdisk (ERI ID) and a registered kernel (EKI ID). The resulting image will associate the three images. 

You can also bundle the root file system independently and associate the ramdisk and kernel with the resulting EMI at run time. 

To add a root filesystem to Walrus: 

Use the following three commands: 

    euca-bundle-image -i <root_filesystem_file> -r <architecture>
    euca-upload-bundle -b <root_filesystem_file_bucket> -m /tmp/<root_filesystem_file>.manifest.xml
    euca-register <root_filesystem_file_bucket>/<root_filesystem_file>.manifest.xml -n <rootfs_name> -a <architecture>

For example: 



    euca-bundle-image -i euca-fedora-10-x86_64/fedora.10.x86-64.img  --ramdisk eri-722B3CBA --kernel eki-5B3D3859 -r x86_64
    ...
    Generating manifest /tmp/fedora.10.x86-64.img.manifest.xml
    
    euca-upload-bundle -b example_rf_bucket -m /tmp/fedora.10.x86-64.img.manifest.xml
    ...
    Generating manifest /tmp/fedora.10.x86-64.img.manifest.xml
    
    euca-register example_rf_bucket/fedora.10.x86-64.img.manifest.xml -n example_rf -a x86_64
    IMAGE	 emi-XXXXXXXX

Where the returned value `emi-XXXXXXXX` is the unique ID of the registered machine image. 

