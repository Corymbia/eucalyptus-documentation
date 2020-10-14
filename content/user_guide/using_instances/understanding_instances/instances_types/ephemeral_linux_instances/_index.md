+++
title = "Ephemeral Linux Instances"
weight = 20
+++

Instance store-backed instances are ephemeral instances. This means that any changes made to a running instance are lost if the instance is either purposely or accidentally terminated. Applications running in ephemeral instances should write their data to persistent storage for safe keeping. Persistent storage available to instances includes Storage Controller volumes and the Walrus. 

As an instance store-backed instance is launched, several files are brought together using loop devices on the Node Controller. As these files are brought together they form what looks like a disk to the instance's operating system. The illustration below lists a some of the files that make up a running instance. Notice that the EKI, EMI, and ERI images are presented to the instance's operating system as the partition */dev/sda1* and are mounted as the */* file system. 




![image]({{< ref "/" >}}images/EC2-Backed-Ephemeral-Instances.png)




Assume that the illustration above shows some of the files that make up an instance that was launched in a vmtype with 2GB of storage. Notice that the *eki-** , *emi-** , and *eri-** files have been downloaded from the Walrus and cached on the Node Controller. These three files consume around 1.06GB of storage space. Notice also that a swap file was automatically created for the instance. The swap file has the string *swap* in its name and the file is approximately 500MB in size. It is presented to the instance's operating system as the partition */dev/sda3* . 

This means the EKI, ERI, EMI, and swap files have consumed approximately 1.5GB of the available 2GB of storage space. The remaining 500GB is allocated to the file with the string *ext3* in its name. In our example, this space is formatted as an ext3 file system and is made available to the instance as the disk partition */dev/sda2* , and is actually mounted to the */mnt* directory in the instance. An example of this configuration is shown below. 




![image]({{< ref "/" >}}images/Ephemeral-Disk-Illustration.png)




