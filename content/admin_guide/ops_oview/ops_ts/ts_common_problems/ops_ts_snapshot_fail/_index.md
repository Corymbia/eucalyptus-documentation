+++
title = "Problem: snapshot creation failed"
weight = 10
+++

On the SC, depending on the backend used for storage: 

* For Overlay, use the command to check the disk space in . 
* For DAS, use the command to check the disk space in the DAS volumes. 
* For any other backend, use its specific commands to check the free space for storage allocated for volumes. 
Is there enough space? 

Yes: On the OSG host, depending on the backend used for object storage: 

* For Walrus, use the command to check the disk space in . 
* For RiakCS or Ceph-RGW, use its specific commands to check the free space for storage allocated for buckets and objects. 
Is there enough space? Yes. 

* Use and note the IP addresses for the OSG and SC. 
* SSH to SC and ping the OSG. Are there error messages? 


No: Delete volumes or add disk space. No: Delete volumes or add disk space. 