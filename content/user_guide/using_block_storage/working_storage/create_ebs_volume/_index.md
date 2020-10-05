+++
title = "Create and Attach an EBS Volume"
weight = 10
+++

The following example shows how to create a 10 gigabyte EBS volume and attach it to a running instance called `i-00000000` running in availability zone `zone1` . 

Create a new EBS volume in the same availability zone as the running instance. 

    euca-create-volume --availability-zone zone1 --size 10

The command displays the ID of the newly-created volume. Attach the newly-created volume to the instance, specifying the local device name `/dev/sdf` . 

    euca-attach-volume vol-00000000 -i i-00000000 -d /dev/sdf

You've created a new EBS volume and attached it to a running instance. You can now access the EBS volume from your running instance. 