+++
title = "Troubleshooting"
weight = 50
+++

This section is presented in a Q&A format to provide a quick reference to the most frequently asked questions. 

1. Can Cloud Administrators federate existing clouds (i.e. clouds that already have non-system Eucalyptus accounts)? **A.** No, this is currently not supported. If a cloud administrator wants to federate an Eucalyptus clouds, this must be done prior to any non-system Eucalyptus account/user/group creation. 


1. Is Eucalyptus DNS required for federating Eucalyptus clouds? **A.** No, however its highly recommended to enable it. 


1. Are supported for more granular IAM access policies per region? **A.** As of 4.2, no. IAM policies apply globally (for all regions). In order to get more granular IAM access, use availability zone restrictions under each region. For more information, see [Restrict Image to Availability Zone](https://github.com/eucalyptus/architecture/wiki/iam-3.4-cluster-policies#Restrict_Image_to_Availability_Zone) . 


1. What services/resources span globally? Which span regionally? **A.** Currently, only Eucalyptus IAM and STS are global services/resources. All other services/resources are region-based (i.e. Eucalyptus cloud-specific). The only resource that can be either global or regional are keypairs. This is because users can import the same keypair to each region, therefore, the keypair is globally accessible. For additional information, please refer to the AWS EC2 Documentation regarding [Resource Locations](http://docs.aws.amazon.com/AWSEC2/latest/UserGuide/resources.html) . 


1. Are Eucalyptus system accounts global in a federated setup? **A.** No. Any Eucalyptus system account is limited to that region. Examples of Eucalyptus system accounts are as follows: 

* eucalyptus 
* (eucalyptus)blockstorage 
* (eucalyptus)aws-exec-read 
* (eucalyptus)cloudformation 



1. Is and supported? **A.** No. There have been no improvements associated with Object Storage Gateway (OSG) regarding cross-regional behavior similar to AWS. 


1. If a user uploads an object to an Object Storage Gateway in one region, will copies show up in other regions (similar to the behavior on AWS)? **A.** No, this is currently unsupported. 


1. Do federated Eucalyptus clouds follow the same globally? **A.** No, Eucalyptus IAM limitations are regionally scoped. 




