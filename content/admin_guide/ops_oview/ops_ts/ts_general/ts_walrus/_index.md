+++
title = "Walrus and Storage"
weight = 10
+++

This topic contains information about Walrus-related problems and solutions.
Walrus decryption failed.
 On Ubuntu 10.04 LTS, kernel version 2.6.32-31 includes a bug that prevents Walrus from decrypting images. This can be determined from the following line in cloud-output.log 

    javax.crypto.
    BadPaddingException: pad block corrupted

If you are running this kernel: 



1. Update to kernel version 2.6.32-33 or higher. 
1. De-register the failed image ( ). 
1. Re-register the bundle that you uploaded ( ). 

Walrus physical disk is not large enough.
 

1. Stop the CLC. 
1. Add a disk. 
1. Migrate your data. 
Make sure you use LVM with your new disk drive(s). 


