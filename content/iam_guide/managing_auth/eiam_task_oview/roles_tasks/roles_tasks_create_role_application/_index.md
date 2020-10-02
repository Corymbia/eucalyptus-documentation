+++
title = "Launch an Instance with a Role"
weight = 10
hidden = true
+++

To create a role for a Eucalyptus instance, you must first create a trust policy that you can use for it. 
## Create Trust Policy
You can create trust policies in two ways: 



* a file method 
* a command line method 

## Create trust policy using a file
Create a trust policy file with the contents below and save it in a text file called `role-trust-policy.json` : 
    {
      "Version": "2012-10-17",
      "Statement": [
        {
          "Effect": "Allow",
          "Principal": { "Service": "ec2.amazonaws.com"},
          "Action": "sts:AssumeRole"
        }
      ]
    }

Create the role using the `euare-rolecreate` command, specifying the trust policy file that was previously created: 
    
    # euare-rolecreate --role-name describe-instances -f role-trust-policy.json
    # euare-rolelistbypath 
    arn:aws:iam::408396244283:role/describe-instances

Proceed with applying an access policy to a role. 
## Create trust policy using the command line
The other way to create the role is to use the command line options to specify the trust policy:Issue the following string on the command line: 
    
    # euare-rolecreate --role-name describe-instances --service http://compute.acme.eucalyptus-systems.com:8773/
    # euare-rolelistbypath 
    arn:aws:iam::408396244283:role/describe-instances

Proceed with applying an access policy to a role. 
## Create and apply an access policy to a role
Create a policy and save it in a text file with a `.json` extension. The following example shows a policy that allows listing the contents of an S3 bucket called "mybucket": 
    {
      "Statement": [
        {
          "Action": [
            "s3:ListBucket"
          ],
          "Effect": "Allow",
          "Resource": "arn:aws:s3:::mybucket"
        }
      ]
    }


{{% notice note %}}
For more information on policies, see . 
{{% /notice %}}
Apply the access policy to the role using the `euare-roleuploadpolicy` command, passing in the filename of the policy you created in the previous step: `euare-roleuploadpolicy --role-name mytestrole --policy-name s3-list-bucket --policy-document my-test-policy.json` 