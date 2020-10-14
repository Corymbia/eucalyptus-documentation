+++
title = "Assume a Role"
weight = 30
+++

A role is assigned a specific set of tasks and permissions. Users may assume a different role than the one they have in order to perform a different set of tasks. For example, the primary administrator is unavailable and the backup administrator is asked to assume the role of the primary administrator during his or her absence. A few points to consider before assuming a role: 

* A role must first be set up by an administrator. 
* You must log in as an IAM user, not as an account root user. 
* Once you assume another role, you temporarily give up your existing user permissions and assume the permissions of your new role. 
* When you are no longer assuming another role, your usual user permissions are automatically restored. 



## Create Role
The scenario described in this section outlines the procedure for creating a role in order to delegate permissions to an IAM user.Create a role that allows users of an account to manage keypairs. Management of keypairs include the following EC2 actions: 



* CreateKeyPair 
* DeleteKeyPair 
* DescribeKeyPairs 
* ImportKeyPair 
Create a role for managing keypairs for the account. In this example, the admin user of 'devops' account (001827830003) is creating the role: 

    # cat devops-role-trustpolicy.json
    {
     "Version": "2012-10-17",
     "Statement": [{
     "Effect": "Allow",
     "Principal": {"AWS": "arn:aws:iam::001827830003:root"},
     "Action": "sts:AssumeRole"
     }]
    }
    
    # euare-rolecreate -f devops-role-trustpolicy.json devops-ec2-keypair-mgmt-role --region devops-admin@future

Add IAM access policy for keypair management to the role: 

    # cat keypair-mgmt-policy.json
    {
      "Version": "2012-10-17",
      "Statement": [
        {
          "Sid": "Stmt1445362739663",
          "Action": [
            "ec2:CreateKeyPair",
            "ec2:DeleteKeyPair",
            "ec2:DescribeKeyPairs",
            "ec2:ImportKeyPair"
          ],
          "Effect": "Allow",
          "Resource": "*"
        }
      ]
    }
    
    # euare-roleuploadpolicy --policy-name ec2-keypair-actions --policy-document keypair-mgmt-policy.json devops-ec2-keypair-mgmt-role --region devops-admin@future

Now that the role has been created, follow the [AWS IAM best practice of using groups to assign permission to IAM users](http://docs.aws.amazon.com/IAM/latest/UserGuide/IAMBestPractices.html#use-groups-for-permissions) and attach an IAM access policy to the group to allow any members (example shows 'user01' user) to assume the 'devops-ec2-keypair-mgmt-role' role: 

    # euare-groupcreate -g Key-Managers --region devops-admin@future
    # euare-groupadduser -u user01 -g Key-Managers --region devops-admin@future
    # cat devops-keypair-mgmt-assume-role-policy.json
    {
     "Version": "2012-10-17",
     "Statement": [{
     "Effect": "Allow",
     "Action": "sts:AssumeRole",
     "Resource": "arn:aws:iam::001827830003:role/devops-ec2-keypair-mgmt-role"
     }]
    }
    # euare-groupuploadpolicy -p keypair-mgmt-role-perm -f devops-keypair-mgmt-assume-role-policy.json Key-Managers --region devops-admin@future

Now that members can assume the 'devops-ec2-keypair-mgmt-role' role, run the following command to list all keypairs under the account: 

    # eval `/usr/bin/euare-assumerole devops-ec2-keypair-mgmt-role --region devops-user01@future`
    # euca-describe-keypairs --region @future
    KEYPAIR	devops-admin	9e:1a:bc:ac:98:b1:97:7c:65:b0:b3:7c:96:f5:d5:7b:a1:3e:36:a6

When done assuming the role, the role must be released using `euare-releaserole` : 

    # eval `/usr/bin/euare-releaserole --region devops-user01@future`


