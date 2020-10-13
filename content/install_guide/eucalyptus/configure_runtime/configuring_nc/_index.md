+++
title = "Configure Node Controller"
weight = 70
+++

On some Linux installations, a sufficiently large amount of local disk activity can slow down process scheduling. This can cause other operations (e.g., network communication and instance provisioning) appear to stall. Examples of disk-intensive operations include preparing disk images for launch and creating ephemeral storage. 

1. Log in to an NC server and open the */etc/eucalyptus/eucalyptus.conf* file. 
1. Change the `CONCURRENT_DISK_OPS` parameter to the number of disk-intensive operations you want the NC to perform at once. 
    1. Set `CONCURRENT_DISK_OPS` to 1 to serialize all disk-intensive operations. Or ...
    1. Set it to a higher number to increase the amount of disk-intensive operations the NC will perform in parallel. 
