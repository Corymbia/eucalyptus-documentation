+++
title = "Roles"
weight = 10
hidden = true
+++

A *role* A role is a mechanism that enables the delegation of access to users or applications. 

A role is associated with an account, and has a set of permissions associated with it that are defined in the form of an IAM *policy* . A policy specifies a set of actions and resources within that account that the role is allowed to access. 
{{% notice note %}}
For more information on policies, see Policy Overview. 
{{% /notice %}}


By assuming a role, a user or an applications gets a set of permissions associated with that role. When a role is assumed, the Eucalyptus STS service returns a set of temporary security credentials that can then be used to make programmatic requests to resources in your account. This eliminates the need to share or hardcode security credentials with applications that need access to resources in your cloud. 

Eucalyptus roles are managed through the Eucalyptus Euare service, which is compatible with Amazon's Identity and Access Management service. For more information on IAM and roles, please see the [Amazon IAM User Guide](http://docs.aws.amazon.com/IAM/latest/UserGuide/WorkingWithRoles.html) . 


## Usage Scenarios for Roles
There are several scenarios in which roles can be useful, including: 

**Applications** 

Applications running on instances in your Eucalyptus cloud will often need access to other resources in your cloud. Instead of creating AWS credentials for each application, or distributing your own credentials,, you can use roles to enable you to delegate permission to the application to make API requests. For more information, see [Launch an Instance with a Role](roles_tasks_create_role_application.dita) . 

**Account Delegation** 

You can use roles to allow one account to access resources owned by another account. IAM Roles under the 'eucalyptus' account can be assumed by users under 'non-eucalyptus' account(s). For example, if you had an 'infrastructure auditing' account, and an audit was needed to be performed on all the cloud resources used on the cloud, a user could assume the 'Resource Administrator' role and audit all the resources used by all the accounts on the cloud. For more information on IAM account delegation, see [Using Roles to Delegate Permissions and Federate Identities](http://docs.aws.amazon.com/IAM/latest/UserGuide/roles-toplevel.html) . Also, go to the walkthrough provided in the [AWS Identity and Access Management](http://docs.aws.amazon.com/IAM/latest/UserGuide/roles-walkthrough-crossacct.html) section of the AWS documentation. 


## Pre-Defined Roles
Eucalyptus offers a number of pre-defined privileged roles. These roles are associated with the `eucalyptus` account, and have privileges to manage resources across the cloud and non-privileged accounts. Only the eucalyptus account can manage or modify these roles. 

To see the pre-defined roles, use `euare-rolelistbypath` with the credentials of a user that is part of the `eucalyptus` account. For example: 


    # euare-rolelistbypath 
    arn:aws:iam::944786667073:role/eucalyptus/AccountAdministrator
    arn:aws:iam::944786667073:role/eucalyptus/InfrastructureAdministrator
    arn:aws:iam::944786667073:role/eucalyptus/ResourceAdministrator

**Account Administrator** 

The Account Administrator (AA) can manage Eucalyptus accounts. To view the policy associated with the Account Administrator role, use `euare-rolelistpolicies` with the credentials of a user that is part of the `eucalyptus` account. For example: 


    # euare-rolelistpolicies --role-name AccountAdministrator --verbose
    AccountAdministrator
    {
      "Statement":[ {
        "Effect": "Allow",
        "Action": [
          "iam:*"
        ],
        "NotResource": "arn:aws:iam::eucalyptus:*",
        "Condition": {
          "Bool": { "iam:SystemAccount": "false" }
        }
      } ]
    }
    IsTruncated: false

**Resource Administrator** 

The Resource Administrator (RA) can manage AWS-defined resources (such as S3 objects, instances, users, etc) across accounts. To view the policy associated with the Resource Administrator role, use `euare-rolelistpolicies` with the credentials of a user that is part of the `eucalyptus` account. For example: 


    # euare-rolelistpolicies --role-name ResourceAdministrator --verbose
    ResourceAdministrator
    {
      "Statement":[ {
        "Effect": "Allow",
        "Action": [
          "autoscaling:*",
          "cloudwatch:*",
          "ec2:DescribeInstanceAttribute",
          "ec2:DescribeInstances",
          "ec2:DescribeInstanceStatus",
          "ec2:DescribeInstanceTypes",
          "ec2:GetConsoleOutput",
          "ec2:GetPasswordData",
          "ec2:ImportInstance",
          "ec2:ModifyInstanceAttribute",
          "ec2:MonitorInstances",
          "ec2:RebootInstances",
          "ec2:ReportInstanceStatus",
          "ec2:ResetInstanceAttribute",
          "ec2:RunInstances",
          "ec2:StartInstances",
          "ec2:StopInstances",
          "ec2:TerminateInstances",
          "ec2:UnmonitorInstances",
          "ec2:*AccountAttributes*",
          "ec2:*Address*",
          "ec2:*AvailabilityZones*",
          "ec2:*Bundle*",
          "ec2:*ConversionTask*",
          "ec2:*CustomerGateway*",
          "ec2:*DhcpOptions*",
          "ec2:*ExportTask*",
          "ec2:*Image*",
          "ec2:*InternetGateway*",
          "ec2:*KeyPair*",
          "ec2:*NetworkAcl*",
          "ec2:*NetworkInterface*",
          "ec2:*PlacementGroup*",
          "ec2:*ProductInstance*",
          "ec2:*Region*",
          "ec2:*ReservedInstance*",
          "ec2:*Route*",
          "ec2:*SecurityGroup*",
          "ec2:*Snapshot*",
          "ec2:*SpotDatafeedSubscription*",
          "ec2:*SpotInstance*",
          "ec2:*SpotPrice*",
          "ec2:*Subnet*",
          "ec2:*Tag*",
          "ec2:*Volume*",
          "ec2:*Vpc*",
          "ec2:*Vpn*",
          "ec2:*VpnGateway*",
          "elasticloadbalancing:*",
          "s3:*"
        ],
        "Resource": "*"
      }, {
        "Effect": "Allow",
        "Action": [
          "iam:Get*",
          "iam:List*"
        ],
        "NotResource": "arn:aws:iam::eucalyptus:*"
      } ]
    }
    IsTruncated: false

**Infrastructure Administrator** 

The Infrastructre Administrator (IA) can perform operations related to cloud setup and management. Typical responibilities include: 



* Installation and configuration (prepare environment, install Eucalyptus, configure Eucalyptus) 
* Monitoring and maintenance (infrastructure supporting the cloud, cloud management layer, upgrades, security patches, diagnostics and troubleshooting) 
* Backup and restoration 
To view the policy associated with the Infrastructure Administrator role, use `euare-rolelistpolicies` with the credentials of a user that is part of the `eucalyptus` account. For example: 


    # euare-rolelistpolicies --role-name InfrastructureAdministrator --verbose
    InfrastructureAdministrator
    {
      "Statement":[ {
        "Effect": "Allow",
        "Action": [
          "euprop:*",
          "euserv:*",
          "euconfig:*",
          "ec2:MigrateInstances"
        ],
        "Resource": "*"
      } ]
    }
    IsTruncated: false

