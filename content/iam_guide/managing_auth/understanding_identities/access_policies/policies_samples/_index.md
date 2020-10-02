+++
title = "Sample Policies"
weight = 10
hidden = true
+++

A few example use cases and associated policies.Here are some example use cases and associated polices. You can edit these polices for your use, or use them as examples of JSON syntax and form. 


{{% notice note %}}
For more information about JSON syntax used with AWS resources, go to . 
{{% /notice %}}

## Examples: Allowing Specific Actions
The following policy allows a user to only run instances and describe things. 


    {
       "Statement":[{
          "Effect":"Allow",
          "Action":["ec2:*Describe*",​"ec2:*Run*"],
          "Resource":"*",
          }
       ]
       }

The following policy allows a user to only list things: 


    {
      "Statement": [
        {
          "Sid": "Stmt1313686153864",
          "Action": [
            "iam:List*"
          ],
          "Effect": "Allow",
          "Resource": "*"
        }
      ]
      }

The following policy grants a generic basic user permission for running instances and describing things. 


    {
      "Statement": [
        {
          "Sid": "Stmt1313605116084",
          "Action": [
            "ec2:AllocateAddress",
            "ec2:AssociateAddress",
            "ec2:AttachVolume",
            "ec2:Authorize*",
            "ec2:CreateKeyPair",
            "ec2:CreateSecurityGroup",
            "ec2:CreateSnapshot",
            "ec2:CreateVolume",
            "ec2:DeleteKeyPair",
            "ec2:DeleteSecurityGroup",
            "ec2:DeleteSnapshot",
            "ec2:DeleteVolume",
            "ec2:Describe*",
            "ec2:DetachVolume",
            "ec2:DisassociateAddress",
            "ec2:GetConsoleOutput",
            "ec2:RunInstances",
            "ec2:TerminateInstances"
            "ec2:ReleaseAddress"
          ],
          "Effect": "Allow",
          "Resource": "*"
        }
      ]
    }


## Examples: Denying Specific Actions
The following policy allows a user to do anything but delete. 


    {
      "Statement": [
        {
          "Action": [
            "ec2:Delete*"
          ],
          "Effect": "Deny",
          "Resource": "*"
        }
      ]
      }

The following policy denies a user from creating other users. 


    {
      "Statement": [
        {
          "Sid": "Stmt1313686153864",
          "Action": [
            "iam:CreateUser"
          ],
          "Effect": "Deny",
          "Resource": "*"
        }
      ]
    }


## Examples: Specifying Time Limits
The following policy allows a user to run instances within a specific time. 


    {
      "Statement": [
        {
          "Sid": "Stmt1313453084396",
          "Action": [
            "ec2:RunInstances"
          ],
          "Effect": "Allow",
          "Resource": "*",
          "Condition": {
            "DateLessThanEquals": {
              "aws:CurrentTime": "2011-08-16T00:00:00Z"
            }
          }
        }
      ]
    }

The following policy blocks users from running instances at a specific time. 


    {
      "Statement": [
        {
          "Sid": "Stmt1313453084396",
          "Action": [
            "ec2:RunInstances"
          ],
          "Effect": "Allow",
          "Resource": "*",
          "Condition": {
            "DateLessThanEquals": {
              "aws:CurrentTime": "2011-08-16T00:00:00Z"
            }
          }
        }
      ]
      }

The following policy keeps alive an instance for 1,000 hours (60,000 minutes). 


    {
      "Statement": [
        {
          "Action": ["ec2:RunInstances" ],
          "Effect": "Allow",
          "Resource": "*",
          "Condition": { "NumericEquals":{"ec2:KeepAlive":"60000"}}
        }
      ]
      }

The following policy sets an expiration date on running instances. 


    {
      "Statement": [
        {
          "Action": ["ec2:RunInstances" ],
          "Effect": "Allow",
          "Resource": "*",
          "Condition": { "DateEquals":{"ec2:ExpirationTime":"2011-08-16T00:00:00Z"}}
        }
      ]
    }


## Examples: Restricting Resources
The following policy allows users to only launch instances with a large image type. 


    {
      "Statement": [
        {
          "Action": [
            "ec2:RunInstances"
          ],
          "Effect": "Allow",
          "Resource": "arn:aws:ec2:::vmtype/m1.xlarge"
        }
      ]
      }

The following policy restricts users from launching instances with a specific image ID. 


    {
      "Statement": [
        {
          "Action": [
            "ec2:RunInstances"
          ],
          "Effect": "Deny",
          "Resource": "arn:aws:ec2:::image/emi-0FFF1874"
        }
      ]
      }

The following policy restricts users from allocating addresses to a specific elastic IP address. 


    {
      "Statement": [
        {
          "Sid": "Stmt1313626078249",
          "Action": "*",
          "Effect": "Deny",
          "Resource": "arn:aws:ec2:::address/192.168.10.140"
        }
      ]
      }

The following policy denies volume access. 


    {
      "Statement": [
        {
          "Action": [
            "ec2:*"
          ],
          "Effect": "Deny",
          "Resource": "arn:aws:ec2:::volume/*"
        }
      ]
       
    }


{{% notice note %}}
For policies attached to an account, quota limits can be specified. See the Quotas section for further details. 
{{% /notice %}}
