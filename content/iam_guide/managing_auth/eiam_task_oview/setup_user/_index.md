+++
title = "Use Case: Create a User"
weight = 20
+++

This use case details tasks needed to create a user with limited access. 


## Create a Group
We recommend that you apply permissions to groups, not users. In this example, we will create a group for users with limited access. 

Enter the following command to create a group for users who will be allowed create snapshots of volumes in Eucalyptus. 

    euare-groupcreate -g ebs-backup

Open an editor and enter the following JSON policy: 

    {
      "Statement": [
        {
          "Action": [
            "ec2:CreateSnapshot"
          ],
          "Effect": "Allow",
          "Resource": "*"
        }
      ]
    }

Save and close the file. Enter the following to add the new policy name `allow-snapshot` and the JSON policy file to the `ebs-backup` group: 

    euare-groupuploadpolicy -g ebs-backup -p allow-snapshot -f allow-snapshot.json


## Create the User
Create the user for the group with limited access. 

Enter the following command to create the user `sam` in the group `ebs-backup` and generate a new key pair for the user: 

    euare-usercreate -u sam -g ebs-backup -k

Eucalyptus responds with the access key ID and the secret key, as in the following example: 

    AKIAJ25S6IJ5K53Y5GCA
    QLKyiCpfjWAvlo9pWqWCbuGB9L3T61w7nYYF057l

