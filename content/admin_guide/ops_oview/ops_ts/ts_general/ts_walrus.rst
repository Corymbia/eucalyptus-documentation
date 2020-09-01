+++
title = "Walrus and Storage"
weight = 5
+++

..  _ts_walrus:

This topic contains information about Walrus-related problems and solutions.

**Walrus decryption failed.**
	On Ubuntu 10.04 LTS, kernel version 2.6.32-31 includes a bug that prevents Walrus from decrypting images. This can be determined from the following line in cloud-output.log 

.. code::

  javax.crypto.
  BadPaddingException: pad block corrupted

If you are running this kernel: 



* Update to kernel version 2.6.32-33 or higher. 

* De-register the failed image ( ). 

* Re-register the bundle that you uploaded ( ). 



**Walrus physical disk is not large enough.**
	

* Stop the CLC. 

* Add a disk. 

* Migrate your data. 

Make sure you use LVM with your new disk drive(s). 



