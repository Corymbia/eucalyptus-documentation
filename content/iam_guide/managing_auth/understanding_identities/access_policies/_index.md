+++
title = "Policy Overview"
weight = 5
chapter = true
+++


## Policy Overview
Eucalyptus uses the policy language to specify user level permissions as AWS IAM. Policies are written in JSON. Each policy file can contain multiple statements, each specifying a permission.A permission statement specifies whether to allow or deny a list of actions to be performed on a list of resources, under specific conditions. 

A permission statement has the following components: 



* Begins the decision that applies to all following components. Either: or 
* Indicates service-specific and case-sensitive commands. For example: 
* Indicates selected resources, each specified as an Amazon resource name (ARN). For example: 
* Indicates additional constraints of the permission. For example: 
The following policy example contains a statement that gives a user with full permission. This is the same access as the account administrator: 


    {
      "Version":"2011-04-01",
     	"Statement":[{
     	  "Sid":"1",
     	  "Effect":"Allow",
     	  "Action":"*",
     	  "Resource":"*"
     	}]
    }

For more information about policy language, go to the [IAM User Guide](http://docs.amazonwebservices.com/IAM/latest/UserGuide/PermissionsOverview.html) . 


## Policy Notes
You can combine IAM policies with account level permissions. For example, the admin of account A can give users in account B permission to launch one of account A’s images by changing the image attributes. Then the admin of account B can use IAM policy to designate the users who can actually use the shared images. 

You can attach IAM policies to both users and groups. When attached to groups, a policy is equivalent to attaching the same policy to the users within that group. Therefore, a user might have multiple policies attached, both policies attached to the user, and policies attached to the group that the user belongs to. 

Do not attach IAM policies (except quota policies, a Eucalyptus extension) to account admins. At this point, doing so won’t result in a failure but may have unexpected consequences. 

