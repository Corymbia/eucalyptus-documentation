+++
title = "Policy Extensions"
weight = 10
+++

Eucalyptus extends the IAM policy in order to meet the needs of enterprise customers.
## EC2 Resource
In IAM, you cannot specify EC2 resources in a policy statement except a wildcard, `“*”` . So, you can't restrict a permission to specific EC2 entities. For example, you can't restrict a user to run instances on a specific image or VM type. To solve that, Eucalyptus created the EC2 resource for the policy language. The following example shows the ARN of an EC2 resource. 



    arn:aws:ec2::<account_id>:<resource_type>/<resource_id>

Where account id is optional. 

Eucalyptus supports the following resource types for EC2: 



* image 
* securitygroup 
* address (either an address or address range: 192.168.7.1-192.168.7.255) 
* availabilityzone 
* instance 
* keypair 
* volume 
* snapshot 
* vmtype 
The following example specifies permission to launch instances with only an m1.small VM type: 



    {
      "Version":"2011-04-01",
      "Statement":[{
        "Sid":"2",
        "Effect":"Allow",
        "Action":"ec2:RunInstances",
        
        "Resource": [
        "arn:aws:ec2:::vmtype/m1.small",
        "arn:aws:ec2:::image/*",
        "arn:aws:ec2:::securitygroup/*",
        "arn:aws:ec2:::keypair/*",
        "arn:aws:ec2:::availabilityzone/*",
        "arn:aws:ec2:::instance/*"
    ]
    
      }]
    }


## Policy Key
Eucalyptus implements the following AWS policy keys: 



* aws:CurrentTime 
* aws:SourceIp 
* aws:TokenIssueTime 
* aws:SecureTransport 
* ec2:SourceInstanceARN 
Eucalyptus extends the policy keys by adding the following to the lifetime of an instance: 



* ec2:KeepAlive: specifies the length of time (in minutes) that an instance can run 
* ec2:ExpirationTime: specifies the expiration time (in minutes) for an instance 
For more information about policy keys, see the AWS documentation, [IAM Policy Elements Reference](http://docs.aws.amazon.com/IAM/latest/UserGuide/reference_policies_elements.html) . 

The following example restricts an instance running time to 24 hours: 



    {
      "Version":"2011-04-01",
      "Statement":[{
        "Sid":"3",
        "Effect":"Allow",
        "Action":"ec2:RunInstances",
        "Resource":"*",
        "Condition":{
          “NumericEquals”:{
            “ec2:KeepAlive”:”1440”
          }
        }
      }]
    }

If there are multiple `ec2:KeepAlive` or `ec2:ExpirationTime` keys that match a request, Eucalyptus chooses the longer lifetime for the instance to run. 

For more use cases, such as setting up temporary permissions, see the AWS documentation, [Disabling Permissions for Temporary Security Credentials](http://docs.aws.amazon.com/IAM/latest/UserGuide/id_credentials_temp_control-access_disable-perms.html) . 

