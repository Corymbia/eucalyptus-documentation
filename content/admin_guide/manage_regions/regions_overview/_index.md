+++
title = "Regions Overview"
weight = 10
+++

Eucalytpus provides support for the notion of federation of identity.Federation of identity information means that a Cloud Administrator can create a federation of (otherwise independent) Eucalyptus "clouds" where a Cloud User, using the same credentials as always, can use any of these federated Eucalyptus cloud regions. For the parts of Identify Access Management (IAM) and Security Token Service (STS) that Eucalyptus implements, the experience exposed to the Cloud User is the same as that seen by an AWS user working across AWS regions. 

A user can interact with any region using the same credentials, subjected to the same policies, and having uniformly accessible and structured principals (Accounts, Users, Groups, Roles, etc.). The globality also includes the STS service functionality, the temporary credentials produced by the STS service also work globally. 

Notably, this feature is restricted to IAM/STS and does not include other services which have pseudo-global characteristics, such as global bucket name space for S3. The following are general principles associated with regions: 

* A region needs to be Registered as a federated region 
* Registered regions should be discoverable via the EC2 DescribeRegions response 
* A cloud user's credentials should be accepted by any federated cloud 
* There is a global IAM service (identities and policies are global for all registered regions) 




