+++
title = "Manage IAM Resources"
weight = 10
+++

To manage Euare (IAM) resources on your Eucalyptus cloud, use the option with any command that describes, adds, deletes, or modifies resources. This option allows you to assume the role of the admin user for a given account. You can also use a policy to control and limit instances to specific availability zones.The following are some examples. For more information about IAM commands, see [](../euca2ools-guide/eiam.dita) . 

To list all groups in an account, enter the following command: 
    euare-grouplistbypath --as-account <account-name>

To list all users in an account, enter the following command: 
    euare-userslistbypath --as-account <account-name>

To delete the login profile of a user in an account, enter the following command: 
    euare-userdelloginprofile --as-account <account-name> -u <user_name>

To modify the login profile of a user in an account, enter the following command: 
    euare-usermod --as-account <account-name> -u <user_name> -n
    <new_user_name>

To restrict an image to a specific availability zone, edit and attach this sample policy to a user: 
    {
        "Statement":[
          {
            "Effect":"Allow",
            "Action":"ec2:*",
             "Resource":"*"
          },
          {
            "Effect": "Deny",
            "Action": [ "ec2:*" ],
            "Resource": "arn:aws:ec2:::availabilityzone/PARTI00",
            "Condition": {
              "ArnLike": {
                "ec2:TargetImage": "arn:aws:ec2:*:*:image/emi-239D37F2"
              }
            }
          }
        ]
      }

To restrict a user to actions only within a specific availability zone, edit and attach this sample policy to a user: 
    {
        "Version": "2012-10-17",
        "Statement": [{
          "Effect": "Allow",
          "Action": [ "ec2:TerminateInstances" ],
          "Resource": "*",
          "Condition": {
            "StringEquals": {
              "ec2:AvailabilityZone": "PARTI00"
            }
          }
        }]
      }

To deny actions at the account level, edit and attach this example policy to an account: 
    {
        "Statement": [ {
          "Effect": "Deny",
          "Action": [ "ec2:RunInstances" ],
          "Resource": "arn:aws:ec2:::availabilityzone/PARTI00",
          "Condition": {
              "ArnLike": {
                  "ec2:TargetImage": "arn:aws:ec2:*:*:image/emi-239D37F2"
              }
          }
        } ]
      }

