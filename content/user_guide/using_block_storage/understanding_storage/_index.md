+++
title = "EBS Overview"
weight = 5
+++

Eucalyptus Elastic Block Storage (EBS) provides block-level storage volumes that you can attach to instances running in your Eucalyptus cloud. An EBS volume looks like any other block-level storage device when attached to a running Eucalyptus instance, and may be formatted with an appropriate file system and used as you would a regular storage device. Any changes that you make to an attached EBS volume will persist after the instance is terminated. 

You can create an EBS volume by using the Eucalyptus command line tools or by using the Eucalyptus management console and specifying the desired size (up to 10GB) and availability zone. Once you've created an EBS volume, you can attach it to any instance running in the same availability zone. An EBS volume can only be attached to one running instance at a time, but you can attach multiple EBS volumes to a running instance. 

You can create a backup — called a *snapshot* — of any Eucalyptus EBS volume. You can create a snapshot by using the command-line tools or the Eucalyptus management console and simply specifying the volume from which you want to create the snapshot, along with a description of the snapshot. Snapshots can be used to create new volumes. 

