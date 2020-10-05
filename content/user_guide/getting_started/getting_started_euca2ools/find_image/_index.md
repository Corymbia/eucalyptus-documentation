+++
title = "Find an Image"
weight = 10
+++

To find an image: 

Enter the following command: 

    euca-describe-images

The output displays all available images. 

    IMAGE	emi-EC1410C1	centos-32/centos.5-3.x86.img.manifest.xml ↵
    admin	available	public 	x86_64	machine
    IMAGE	eki-822C1344	kernel-i386/vmlinuz-2.6.28-11-server.manifest.xml ↵
    admin	available	public 	x86_64	kernel
    IMAGE	eri-A98C13E4  initrd-64/initrd.img-2.6.28-11-generic.manifest.xml ↵
    admin	available	public 	x86_64	ramdisk

Look for the image ID in the second column and write it down. The image ID starts with `emi-` . Once you find a suitable image to use, make sure you have a keypair to use. 
