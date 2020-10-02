+++
title = "Algorithms"
weight = 10
hidden = true
+++

This topic describes the algorithms used by Eucalyptus to determine access.
## Policy Evaluation Algorithm
You can associated multiple policies and permission statements with a user. The way these are combined together to control the access to resources in an account is defined by the policy evaluation algorithm. Eucalyptus implements the [same policy evaluation algorithm as AWS IAM](http://docs.aws.amazon.com/IAM/latest/UserGuide/AccessPolicyLanguage_EvaluationLogic.html) : 



1. If the request user is account admin, access is allowed. 
1. Otherwise, collect all the policy statements associated with the request user (attached to the user and all the groups the user belongs to), which match the incoming request (i.e. based on the API being invoked and the resources it is going to access). 

## Access Evaluation Algorithm
Now we give the overall access evaluation combining both account level permissions and IAM permissions, which decides whether a request is accepted by Eucalyptus: 



1. If the request user is sys admin, access is allowed. 
1. Otherwise, check account level permissions, e.g. image launch permission, to see if the request user’s account has access to the specific resources. 

## Quota Evaluation Algorithm
Like the normal IAM policies, a user may be associated with multiple quota policies (and multiple quota statements). How all the quota policies are combined to take effect is defined by the quota evaluation algorithm: 



1. If the request user is sys admin, there is no limit on resource usage. 
1. Otherwise, collect all the quotas associated with the request user, including those attached to the request user’s account and those attached to the request user himself/herself (for account admin, we only need collect account quotas). 
1. Evaluate each quota one by one. Reject the request as long as there is one quota being exceeded by the request. Otherwise, accept the request. 

{{% notice note %}}
The hard limits on some resources override quota limits. For example, (system property) overrides the (quota key). 
{{% /notice %}}
