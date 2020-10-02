+++
title = "Manage Walrus Resources"
weight = 10
+++

This topic explains Walrus resources.

* Access Control Lists (ACLs) allow an account to explicitly grant access to a bucket or object to another account. ACLs only work between accounts, not IAM users. You specify accounts with the CanonicalID or the email address associated with the account (for Eucalyptus this is the email of the account admin). 
* These are set by the admin of an account to control the access of users within that specific account. This is how an admin controls what users in that specific account are allowed to do. Policies can specify allow/deny on specific S3 operations (e.g. s3:GetObject, or s3:PutObject). IAM policies are set by sending the policy to the IAM (Euare) endpoint, not S3 (Walrus). 
* These are IAM-like policies set by the bucket owner are not supported in Eucalyptus. 
For more information about bucket ACLs, go to [Access Control List (ACL) Overview](http://docs.aws.amazon.com/AmazonS3/latest/dev/ACLOverview.html) and [Managing ACLs Using the REST API](http://docs.aws.amazon.com/AmazonS3/latest/dev/acl-using-rest-api.html) . 

For more information about IAM policies, go to [Using IAM Policies](http://docs.aws.amazon.com/AmazonS3/latest/dev/UsingIAMPolicies.html) . 

