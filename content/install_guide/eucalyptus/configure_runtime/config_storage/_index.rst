+++
title = "Configure Eucalyptus Storage"
weight = 5
chapter = true
+++

..  _concept_template:



==================
Configure Storage
==================

These are the types of storage available for your Eucalyptus cloud.Object storage Eucalyptus provides an AWS S3 compatible object storage service that provides users with web-based general purpose storage, designed to be scalable, reliable and inexpensive. You choose the object storage backend provider: Walrus or Riak. The Object Storage Gateway (OSG) provides access to objects via the backend provider you choose. 

Block storage Eucalyptus provides an AWS EBS compatible block storage service that provides block storage for EC2 instances. Volumes can be created as needed and dynamically attached and detached to instances as required. EBS provides persistent data storage for instances: the volume, and the data on it, can exist beyond the lifetime of an instance. You choose the block storage backend provider, which can be using freely available resources in your cloud, or via a SAN, if you have a subscription (paid). 

