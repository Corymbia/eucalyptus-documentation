+++
title = "Plan Disk Space"
weight = 5
+++

..  _space_verifying:

We recommend that you choose a disk for the Walrus that is large enough to hold all objects and buckets you ever expect to have, including all images that will ever be registered to your system, plus any Amazon S3 application data. For heavy S3 usage, Riak CS is a better choice for object storage. 

{{% notice note %}}We recommend that you use LVM (Logical Volume Manager). If you run out of disk space, LVM allows you to add disks and migrate the data. {{% /notice %}}

.. list-table::
  :header-rows: 1

  *
    - Service
    - Directory
    - Minimum Size
  *
    - Cloud Controller (CLC)CLC logging
    - /var/lib/eucalyptus/db/var/log/eucalyptus
    - 20GB2GB
  *
    - WalrusWalrus logging
    - /var/lib/eucalyptus/bukkits/var/log/eucalyptus
    - 250GB2GB
  *
    - Storage Controller (SC) (EBS storage) This disk space on the SC is only required if you are not using a SAN driver or if you are using Direct Attached Storage (DAS). For more information, see .
    - /var/lib/eucalyptus/volumes/var/log/eucalyptus
    - 250GB
  *
    - User-Facing Services (UFS)UFS logging
    - /var/lib/eucalyptus/var/log/eucalyptus
    - 5GB 2GB
  *
    - Management ConsoleConsole logging
    - /var/log/eucalyptus-console
    - 5GB 2GB
  *
    - Cluster Controller (CC)CC logging
    - /var/lib/eucalyptus/CC/var/log/eucalyptus
    - 5GB2GB
  *
    - Node Controller (NC)NC logging
    - /var/lib/eucalyptus/instances/var/log/eucalyptus
    - 250GB2GB


If necessary, create symbolic links or mount points to larger filesystems from the above locations. Make sure that the 'eucalyptus' user owns the directories. 

