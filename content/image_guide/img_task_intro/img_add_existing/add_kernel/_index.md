+++
title = "Add a Kernel"
weight = 10
+++

When you add a kernel to Walrus, you bundle the kernel file, upload the file to a bucket in Walrus that you name, and then register the kernel with Eucalyptus. 

To add a kernel to Walrus: 

Use the following three commands: 

    euca-bundle-image -i <kernel_file> --kernel true --arch <architecture>
    euca-upload-bundle -b <kernel_bucket> -m /tmp/<kernel_file>.manifest.xml
    euca-register <kernel_bucket>/<kernel_file>.manifest.xml -a x86_64 -n mynewkernel

For example: 



    euca-bundle-image -i euca-fedora-10-x86_64/xen-kernel/vmlinuz-2.6.27.21-0.1-xen --kernel true --arch x86_64
    ...
    Generating manifest /tmp/vmlinuz-2.6.27.21-0.1-xen.manifest.xml
    
    euca-upload-bundle -b example_kernel_bucket -m /tmp/vmlinuz-2.6.27.21-0.1-xen.manifest.xml
    ...
    Uploaded image as example_kernel_bucket/vmlinuz-2.6.27.21-0.1-xen.manifest.xml
    
    euca-register example_kernel_bucket/vmlinuz-2.6.27.21-0.1-xen.manifest.xml -a x86_64 -n mynewkernel
    IMAGE	eki-XXXXXXXX

Where the returned value `eki-XXXXXXXX` is the unique ID of the registered kernel image. 

