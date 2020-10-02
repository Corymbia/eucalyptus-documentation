+++
title = "Quotas"
weight = 10
+++

Eucalyptus adds quota enforcement to resource usage. To avoid introducing another configuration language into Eucalyptus, and simplify the management, we extend the IAM policy language to support quotas.The only addition added to the language is the new `limit` effect. If a policy statement’s `effect` is `limit` , it is a quota statement. 

A quota statement also has action and resource fields. You can use these fields to match specific requests, for example, quota only being checked on matched requests. The actual quota type and value are specified using special quota keys, and listed in the `condition` part of the statement. Only condition type `NumericLessThanEquals` can be used with quota keys. 


{{% notice note %}}
An account can only have a quota policy. Accounts can only accept IAM policies where Effect is "Deny" or "Limit". If you attach an IAM policy to an account where the Effect is "Allow", you will get unexpected results. 
{{% /notice %}}
The following quota policy statement limits the attached user to only launch a maximum of 16 instances in an account. 


    {
     "Version":"2011-04-01",
     "Statement":[{
       "Sid":"4",
       "Effect":"Limit",
       "Action":"ec2:RunInstances",
       "Resource":"*",
       "Condition":{
         “NumericLessThanEquals”:{
           “ec2:quota-vminstancenumber”:”16”
         }
       }
     }]
    }

You can attach quotas to both users and accounts, although some of the quotas only apply to accounts. Quota attached to groups will take no effect. 

When a quota policy is attached to an account, it actually is attached to the account administrator user. Since only system administrator can specify account quotas, the account administrator can only inspect quotas but can't change the quotas attached to herself. 

The following is all the quota keys implemented in Eucalyptus: 



| Quota Key | Description | Applies to | 
|  :---- |  :---- |  :---- | 
| autoscaling:quota-autoscalinggroupnumber | The number of Autoscaling Groups | account and user | 
| autoscaling:quota-launchconfigurationnumber | Number of Autoscaling Group Launch Configurations | account and user | 
| autoscaling:quota-scalingpolicynumber | Number of Autoscaling Group Scaling Policies | account and user | 
| cloudformation:quota-stacknumber | Number of Cloudformation stacks allowed to create | account | 
| ec2:quota-addressnumber | Number of elastic IPs | account and user | 
| ec2:quota-cputotalsize | Number of Total CPUs Used by EC2 Instances | account and user | 
| ec2:quota-disktotalsize | Number of Total Disk Space (in GB) of EC2 Instances | account and user | 
| ec2:quota-imagenumber | Number of EC2 images | account and user | 
| ec2:quota-internetgatewaynumber | Number of EC2 VPC Internet Gateways | account and user | 
| ec2:quota-memorytotalsize | Number of Total Amount of Memory Used by EC2 Instances | account and user | 
| ec2:quota-securitygroupnumber | Number of EC2 security groups | account and user | 
| ec2:quota-snapshotnumber | Number of EC2 snapshots | account and user | 
| ec2:quota-vminstancenumber | Number of EC2 instances | account and user | 
| ec2:quota-vminstanceactivenumber | Number of EC2 Instances Using Node Resources (pending, running, shutting-down, etc.) | account and user | 
| ec2:quota-volumenumber | Number of EC2 volumes | account and user | 
| ec2:quota-volumetotalsize | Number of total volume size, in GB | account and user | 
| ec2:quota-vpcnumber | Number of EC2 VPCs | account and user | 
| elasticloadbalancing:quota-loadbalancernumber | Number of Elastic Load Balancers | account | 
| iam:quota-groupnumber | Number of IAM groups | account | 
| iam:quota-instanceprofilenumber | Number of IAM Instance Profiles | account and user | 
| iam:quota-rolenumber | Number of IAM Roles | account and user | 
| iam:quota-servercertificatenumber | Number of IAM Server Certificates | account and user | 
| iam:quota-usernumber | Number of IAM users | account | 
| s3:quota-bucketnumber | Number of S3 buckets | account and user | 
| s3:quota-bucketobjectnumber | Number of objects in each bucket | account and user | 
| s3:quota-bucketsize | Size of bucket, in MB | account and user | 
| s3:quota-buckettotalsize | total size of all buckets, in MB | account and user | 


## Default Quota
Contrary to IAM policies, by default, there is no quota limits (except the hard system limit) on any resource allocations for a user or an account. Also, system administrators are not constrained by any quota. Account administrators are only be constrained by account quota. 

