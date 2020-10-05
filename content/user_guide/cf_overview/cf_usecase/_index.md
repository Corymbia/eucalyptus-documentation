+++
title = "CloudFormation Use Case"
weight = 10
+++

This topic describes a use case for creating a stack, checking the stack progress, and deleting the stack.For this use case, we will use the following template: 



    {
      "Parameters": {
        "MyImageId": {
          "Description":"Image id",
          "Type":"String"
        },
        "MyKeyPair": {
          "Description":"Key Pair",
          "Type":"String"
        }
      },
      "Resources" : {
        "MySecurityGroup": {
          "Type": "AWS::EC2::SecurityGroup",
          "Properties": {
            "GroupDescription" : "Security Group with Ingress Rule for MyInstance",
            "SecurityGroupIngress" : [
              {
                "IpProtocol" : "tcp",
                "FromPort" : "22",
                "ToPort" : "22",
                "CidrIp" : "0.0.0.0/0"
              }
            ]
          }
        },
        "MyInstance": {
          "Type": "AWS::EC2::Instance",
          "Properties": {
            "ImageId" : { "Ref":"MyImageId" },
            "SecurityGroups" : [ 
              { "Ref" : "MySecurityGroup" } 
            ],
            "KeyName" : { "Ref" : "MyKeyPair" }
          }
        }
      }
    }

This template creates an instance with a security group that allows global SSH access (port 22), but uses a keypair to log in. It requires two parameters, `MyImageId` , which is the image ID of the instance to create, and `MyKeyPair` , which is the name of the keypair to use to log in with. You can use both values with the `euca-run-instances` command to create an instance manually (for example, `euca-run-instances -k mykey emi-db0b2276` ) so the arguments needed here are standard instance arguments. 

The steps to run this template through the system are explained in the following steps. 


{{% notice note %}}
These steps require that you have an available image (run to verify) and that the CloudFormation service is running (run to verify). 
{{% /notice %}}
Verify connectivity to the CloudFormation service. 

    euform-describe-stacks

You should not see anything returned, including any errors. Create a file called *ex_template.json* that contains the following content: 

    {
      "Parameters": {
        "MyImageId": {
          "Description":"Image id",
          "Type":"String"
        },
        "MyKeyPair": {
          "Description":"Key Pair",
          "Type":"String"
        }
      },
      "Resources" : {
        "MySecurityGroup": {
          "Type": "AWS::EC2::SecurityGroup",
          "Properties": {
            "GroupDescription" : "Security Group with Ingress Rule for MyInstance",
            "SecurityGroupIngress" : [
              {
                "IpProtocol" : "tcp",
                "FromPort" : "22",
                "ToPort" : "22",
                "CidrIp" : "0.0.0.0/0"
              }
            ]
          }
        },
        "MyInstance": {
          "Type": "AWS::EC2::Instance",
          "Properties": {
            "ImageId" : { "Ref":"MyImageId" },
            "SecurityGroups" : [ 
              { "Ref" : "MySecurityGroup" } 
            ],
            "KeyName" : { "Ref" : "MyKeyPair" }
          }
        }
      }
    }

Create a keypair. 

    euca-create-keypair myKey > myKey.pem

Set the permissions on the keypair. 

    chmod 0600 myKey.pem

Find what resources have been created., run the command and the euca-describe-groups commands. Make note of the output for later. Run: 

    euca-describe-instances

Note the output for later use. Run: 

    euca-describe-groups

Note the output for later use. Create the stack. 

    euform-create-stack --template-file ex_template.json -p  MyImageId=<image_id>, MyKeyPair=
     myKey MyStack

Eucalyptus returns output similar to the following: 

    arn:aws:cloudformation::299958418681:stack/MyStack/28fd422b-0836-4374-ade2-eddab2fab3e3

Run the checks you want on your stack. Check the status of the stack. 



    euform-describe-stack
     STACK    MyStack    CREATE_COMPLETE    Complete!   2014-05-30T18:45:54.695Z

Check the stack at any time to see all the events that have occurred during the stack lifecycle. 



    euform-describe-stack-events MyStack
    EVENT  MyStack  40de93ad-1aec-48c3-9c9e-680fe46ce194  AWS::CloudFormation::Stack  
    MyStack  arn:aws:cloudformation::299958418681:stack/MyStack/28fd422b-0836-4374-
    ade2-eddab2fab3e3  2014-05-30T18:45:54.747Z  CREATE_IN_PROGRESS   User Initiated
    EVENT  MyStack  MySecurityGroup-CREATE_IN_PROGRESS-1401475554805   
    AWS::EC2::SecurityGroup   MySecurityGroup   2014-05-30T18:45:54.805Z  CREATE_IN_
    PROGRESS    
    EVENT  MyStack  MySecurityGroup-CREATE_IN_PROGRESS-1401475555003  AWS::EC2::Secu
    rityGroup  MySecurityGroup  MyStack-MySecurityGroup-PSLNKQK0BGY9A   2014-05-30T1
    8:45:55.003Z   CREATE_IN_PROGRESS    
    EVENT  MyStack  MySecurityGroup-CREATE_COMPLETE-1401475555170  AWS::EC2::Securit
    yGroup MySecurityGroup  MyStack-MySecurityGroup-PSLNKQK0BGY9A  2014-05-30T18:45:
    55.17Z CREATE_COMPLETE 
    EVENT  MyStack  MyInstance-CREATE_IN_PROGRESS-1401475555228   AWS::EC2::Instance
    MyInstance   	 2014-05-30T18:45:55.228Z    CREATE_IN_PROGRESS    
    EVENT  MyStack  MyInstance-CREATE_IN_PROGRESS-1401475556078   AWS::EC2::Instance
    MyInstance    i-d141ae0a    2014-05-30T18:45:56.078Z    CREATE_IN_PROGRESS    
    EVENT  MyStack  MyInstance-CREATE_IN_PROGRESS-1401475566466   AWS::EC2::Instance
    MyInstance    i-d141ae0a    2014-05-30T18:46:06.466Z    CREATE_IN_PROGRESS    
    EVENT  MyStack  MyInstance-CREATE_COMPLETE-1401475566507      AWS::EC2::Instance 
    MyInstance    i-d141ae0a    2014-05-30T18:46:06.507Z    CREATE_COMPLETE    
    EVENT  MyStack  26e4445a-2f84-4239-90bf-e34e74fd646f  AWS::CloudFormation::Stack
    MyStack  arn:aws:cloudformation::299958418681:stack/MyStack/28fd422b-0836-4374-a
    de2-eddab2fab3e3 2014-05-30T18:46:06.574Z    CREATE_COMPLETE    Complete!

Run `euca-describe-instances` and `euca-describe-groups` to make sure the new resources have been created. 



    euca-describe-instances
    RESERVATION    r-4ed04891   299958418681   MyStack-MySecurityGroup-PSLNKQK0BGY9A
    INSTANCE    i-d141ae0a    emi-db0b2276   
    euca-10-111-101-87.eucalyptus.g-19-10.autoqa.qa1.eucalyptus-systems.com  euca-1-
    121-167-77.eucalyptus.internal   running   myKey   0   m1.small  2014-05-30T18:4
    5:55.994Z   PARTI00   monitoring-disabled    10.111.101.87    1.121.167.77  
    instance-store   hvm   sg-b4814192   TAG    instance    i-d141ae0a    euca:node 
    10.111.1.135
    
    euca-describe-groups
    GROUP    sg-b4814192    299958418681    MyStack-MySecurityGroup-PSLNKQK0BGY9A   
    Security Group with Ingress Rule for MyInstance    
    PERMISSION    299958418681    MyStack-MySecurityGroup-PSLNKQK0BGY9A  ALLOWS  tcp
    22    22    FROM    CIDR    0.0.0.0/0    ingress

Try to SSH into the instance. 

    ssh -i myKey.pem root@10.111.101.87


{{% notice note %}}
Username might depend on the instance type, and might be root or ubuntu or ec2-user. 
{{% /notice %}}
Delete the stack. 

    euform-delete-stack MyStack

You can run `euca-describe-stacks` and all the other describe commands to check the progress until the delete is complete. Make sure the instance is terminated and that the security group no longer exists. 

