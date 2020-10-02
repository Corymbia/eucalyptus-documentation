+++
title = "CloudFormation Templates"
weight = 10
hidden = true
+++

This topic details templates that have been tested with Eucalyptus.
## AccessKeys.template

    {
      "AWSTemplateFormatVersion":"2010-09-09",
      "Parameters":{
        "Username":{
          "Description":"Username",
          "Type":"String"
        }
      },
      "Resources":{
        "Key1":{
          "Type":"AWS::IAM::AccessKey",
          "Properties":{
            "UserName":{"Ref":"Username"},
            "Serial":"1",
            "Status":"Active"
          }
        },
        "Key2":{
          "Type":"AWS::IAM::AccessKey",
          "Properties":{
            "UserName":{"Ref":"Username"},
           "Serial":"1",
           "Status":"Inactive"
          }
        }
      },
      "Outputs":{
        "Key1AK":{
          "Value":{"Ref":"Key1"}
        },
        "Key1SK":{
          "Value":{"Fn::GetAtt":["Key1","SecretAccessKey"]}
        },
        "Key2AK":{
          "Value":{"Ref":"Key2"}
        },
        "Key2SK":{
          "Value":{"Fn::GetAtt":["Key2","SecretAccessKey"]}
        }
      }
    }


## AutoscalingGroupsAndCloudWatchAlarm.template

    {
      "AWSTemplateFormatVersion":"2010-09-09",
      "Parameters":{
        "ImageId":{
          "Description":"Image id",
          "Type":"String"
        }
      },
      "Resources":{
        "LaunchConfig":{
          "Type":"AWS::AutoScaling::LaunchConfiguration",
          "Properties":{
            "ImageId":{"Ref":"ImageId"},
            "InstanceType":"m1.small",
            "BlockDeviceMappings":[
              {"DeviceName":"/dev/sdc","VirtualName":"ephemeral0"},
              {"DeviceName":"/dev/sdc","Ebs":{"VolumeSize":"10"}}
            ],
            "SecurityGroups":[{"Ref":"InstanceSecurityGroup"}]}
          },
          "ASG1":{
            "UpdatePolicy":{
              "AutoScalingRollingUpdate":{
                "MinInstancesInService":"1",
                "MaxBatchSize":"1",
                "PauseTime":"PT12M5S"
              }
            },
            "Type":"AWS::AutoScaling::AutoScalingGroup",
            "Properties":{
              "AvailabilityZones":{"Fn::GetAZs":{"Ref":"AWS::Region"}
            },
            "LaunchConfigurationName":{"Ref":"LaunchConfig"},
            "MaxSize":"3",
            "MinSize":"1"
          }
        },
        "ScaleUpPolicy":{
          "Type":"AWS::AutoScaling::ScalingPolicy",
            "Properties":{
              "AdjustmentType":"ChangeInCapacity",
              "AutoScalingGroupName":{"Ref":"ASG1"},
              "Cooldown":"1",
              "ScalingAdjustment":"1"
            }
          },
          "CPUAlarmHigh":{
            "Type":"AWS::CloudWatch::Alarm",
            "Properties":{
              "EvaluationPeriods":"1",
              "Statistic":"Average",
              "Threshold":"10",
              "AlarmDescription":"Alarm if CPU too high or metric disappears indicating instance is down",
              "Period":"60",
              "AlarmActions":[{"Ref":"ScaleUpPolicy"}],
              "Namespace":"AWS/EC2",
              "Dimensions":[{
                "Name":"AutoScalingGroupName",
                "Value":{"Ref":"ASG1"}
              }],
              "ComparisonOperator":"GreaterThanThreshold",
              "MetricName":"CPUUtilization"
            }
          },
          "InstanceSecurityGroup":{
            "Type":"AWS::EC2::SecurityGroup",
            "Properties":{
              "GroupDescription":"Cloudformation Group",
              "SecurityGroupIngress":[{
                "IpProtocol":"tcp",
                "FromPort":"22",
                "ToPort":"22",
                 "CidrIp":"0.0.0.0/0"
              }]
            }
          },
          "IngressRule":{
            "Type":"AWS::EC2::SecurityGroupIngress",
            "Properties":{
              "GroupName":{"Ref":"InstanceSecurityGroup"},
              "FromPort":"80",
              "ToPort":"80",
              "IpProtocol":"tcp",
              "SourceSecurityGroupName":{"Ref":"InstanceSecurityGroup"}
          }
        }
      }
    }


## BlockDeviceMappings.template

    {
      "AWSTemplateFormatVersion":"2010-09-09",
      "Description":"Create an EC2 instance running a specified EMI with block device mappings.",
      "Parameters":{
        "ImageId":{
          "Description":"Image id",
          "Type":"String"
        },
        "KeyName":{
          "Description":"KeyName",
          "Type":"String"
        },
        "SnapshotId":{
          "Type":"String"
        }
      },
      "Resources":{
        "Ec2Instance1":{
          "Type":"AWS::EC2::Instance",
          "Properties":{
            "ImageId":{"Ref":"ImageId"},
            "BlockDeviceMappings":[{"DeviceName":"/dev/sdc","VirtualName":"ephemeral0"}]
          }
        },
        "Ec2Instance2":{
          "Type":"AWS::EC2::Instance",
          "Properties":{
            "ImageId":{"Ref":"ImageId"},
            "KeyName":{"Ref":"KeyName"},
            "BlockDeviceMappings":[{
              "DeviceName":"/dev/sdc",
              "Ebs":{"SnapshotId":{"Ref":"SnapshotId"},"DeleteOnTermination":"false"}
            }]
          }
        },
        "Ec2Instance3":{
          "Type":"AWS::EC2::Instance",
          "Properties":{
            "ImageId":{"Ref":"ImageId"},
            "KeyName":{"Ref":"KeyName"},
            "BlockDeviceMappings":[{
              "DeviceName":"/dev/sdc",
              "Ebs":{"VolumeSize":"10","DeleteOnTermination":"true"}
            }]
          }
        }
      }
    }


## ConditionsAndFunctions.template

    {
      "Mappings":{
        "Mapping01":{
          "Key01":{"Value":["1","2"]},
          "Key02":{"Value":"3"},
          "Key03":{"Value":"4"}
        }
      },
      "AWSTemplateFormatVersion":"2010-09-09",
      "Description":"Create an EC2 instance running a specified EMI, also test functions and conditions.",
      "Parameters":{
        "ImageId":{
          "Description":"Image id",
          "Type":"String",
          "NoEcho":"True"
        },
        "Split":{
          "Default":"1,2,3",
          "Type":"CommaDelimitedList"
        }
      },
      "Resources":{
        "Ec2Instance1":{
          "Type":"AWS::EC2::Instance",
            "Properties":{
              "ImageId":{"Ref":"ImageId"}
            },
          "Condition":"True"
        },
        "Ec2Instance2":{
          "Type":"AWS::EC2::Instance",
          "Properties":{
            "ImageId":{"Ref":"ImageId"}
          },
          "Condition":"False"
        }
      },
      "Conditions":{
        "True":{"Fn::Equals":["x","x"]},
        "False":{"Fn::Not":[{"Condition":"True"}]},
        "NotTrue":{"Fn::Not":[{"Condition":"True"}]},
        "NotFalse":{"Fn::Not":[{"Condition":"False"}]},
        "TrueAndTrue":{"Fn::And":[{"Condition":"True"},{"Condition":"True"}]},
        "TrueAndFalse":{"Fn::And":[{"Condition":"True"},{"Condition":"False"}]},
        "FalseAndTrue":{"Fn::And":[{"Condition":"False"},{"Condition":"True"}]},
        "FalseAndFalse":{"Fn::And":[{"Condition":"False"},{"Condition":"False"}]},
        "TrueOrTrue":{"Fn::Or":[{"Condition":"True"},{"Condition":"True"}]},
        "TrueOrFalse":{"Fn::Or":[{"Condition":"True"},{"Condition":"False"}]},
        "FalseOrTrue":{"Fn::Or":[{"Condition":"False"},{"Condition":"True"}]},
        "FalseOrFalse":{"Fn::Or":[{"Condition":"False"},{"Condition":"False"}]}
      },
      "Outputs":{
        "Region":{
          "Value":{"Ref":"AWS::Region"}
        },
        "JoinAndAZ":{
          "Value":{"Fn::Join":[",",{"Fn::GetAZs":""}]}
        },
        "FindInMap1AndSelect":{
          "Value":{"Fn::Select":["0",{"Fn::FindInMap":["Mapping01","Key01","Value"]}]}
        },
        "FindInMap2AndSelect":{
         "Value":{"Fn::Select":["1","Fn::FindInMap":["Mapping01","Key01","Value"]}]}
        },
        "FindInMap3AndSelect":{
          "Value":{"Fn::FindInMap":["Mapping01","Key02","Value"]}
        },
        "FindInMap4AndSelect":{
          "Value":{"Fn::FindInMap":["Mapping01","Key03","Value"]}
        },
        "GetAtt":{
          "Value":{"Fn::GetAtt":["Ec2Instance1","PrivateIp"]}
        },
        "StackId":{
          "Value":{"Ref":"AWS::StackId"}
        },
        "StackName":{
          "Value":{"Ref":"AWS::StackName"}
        },
        "AccountId":{
          "Value":{"Ref":"AWS::AccountId"}
        },
        "True":{
          "Value":{"Fn::Join" : [",",[{"Fn::If": ["True","True","False"]}]]}},
        },
        "False":{
          "Value":{"Fn::Join" : [",",[{"Fn::If": ["False","True","False"]}]]}},
        },
        "NotTrue":{
          "Value":{"Fn::Join" : [",",[{"Fn::If": ["NotTrue","True","False"]}]]}},
        },
        "NotFalse":{
          "Value":{"Fn::Join" : [",",[{"Fn::If": ["NotFalse","True","False"]}]]}},
        },
        "TrueAndTrue":{
          "Value":{"Fn::Join" : [",",[{"Fn::If": ["TrueAndTrue","True","False"]}]]}},
        },
        "TrueAndFalse":{
          "Value":{"Fn::Join" : [",",[{"Fn::If": ["TrueAndFalse","True","False"]}]]}},
        },
        "FalseAndTrue":{
          "Value":{"Fn::Join" : [",",[{"Fn::If": ["FalseAndTrue","True","False"]}]]}},
        },
        "FalseAndFalse":{
          "Value":{"Fn::Join" : [",",[{"Fn::If": ["FalseAndFalse","True","False"]}]]}},
        },
        "TrueOrTrue":{
          "Value":{"Fn::Join" : [",",[{"Fn::If": ["TrueOrTrue","True","False"]}]]}},
        },
        "TrueOrFalse":{
          "Value":{"Fn::Join" : [",",[{"Fn::If": ["TrueOrFalse","True","False"]}]]}},
        },
        "FalseOrTrue":{
          "Value":{"Fn::Join" : [",",[{"Fn::If": ["FalseOrTrue","True","False"]}]]}},
        },
        "FalseOrFalse":{
          "Value":{"Fn::Join" : [",",[{"Fn::If": ["FalseOrFalse","True","False"]}]]}},
        }
      }
    }


## ElasticIP.template
This template attaches an [elastic IP](../shared/glossary.dita#elasticips) to a new and existing instance. You must pass along the existing instance ID. 


    {
      "AWSTemplateFormatVersion":"2010-09-09",
      "Description":"Create an EC2 instance running a specified EMI and some elastic IP addresses.",
      "Parameters":{
        "ImageId":{
          "Description":"Image id",
          "Type":"String"
        },
        "OtherInstanceId":{
          "Description":"Other instance id",
          "Type":"String"
        }
        },
        "Resources":{
          "Ec2Instance1":{
            "Type":"AWS::EC2::Instance",
            "Properties":{
              "ImageId":{"Ref":"ImageId"}
            }
          },
          "EIP1":{
            "Type":"AWS::EC2::EIP",
            "Properties":{
              "InstanceId":{"Ref":"Ec2Instance1"}
            }
          },
          "EIP2":{
            "Type":"AWS::EC2::EIP",
            "Properties":{
            }
          },
          "EIPAssociation2":{
            "Type":"AWS::EC2::EIPAssociation",
            "Properties":{
              "InstanceId":{"Ref":"OtherInstanceId"},
              "EIP":{"Ref":"EIP2"}
            }
          }
        },
        "Outputs":{
          "Output1":{
            "Value":{"Ref":"EIPAssociation2"}
          }
      }
    }


## ElasticLoadBalancer.template
There is a hard-coded image ID in the `Mapping` section here to test `FindInMap` . Change the value to an instance that exists in your cloud. 


    {
      "AWSTemplateFormatVersion":"2010-09-09",
      "Description":"Based on the AWS Cloudformation Sample Template for ELB.  Modify this template, and put the correct emi-XXXX in the value fields with a blank key of the AWSRegionArch2AMI mapping.",
      "Parameters":{
        "InstanceType":{
          "Description":"WebServer EC2 instance type",
          "Type":"String",
          "Default":"m1.small",
          "AllowedValues":["t1.micro","m1.small","m1.medium","m1.large","m1.xlarge","m2.xlarge","m2.2xlarge",
                           "m2.4xlarge","m3.xlarge","m3.2xlarge","c1.medium","c1.xlarge","cc1.4xlarge",
                           "cc2.8xlarge","cg1.4xlarge"],
          "ConstraintDescription":"must be a valid EC2 instance type."
        },
        "WebServerPort":{
          "Description":"TCP/IP port of the web server",
          "Type":"String",
          "Default":"8888"
        },
        "KeyName":{
          "Description":"Name of an existing EC2 KeyPair to enable SSH access to the instances",
          "Type":"String",
          "MinLength":"1",
          "MaxLength":"255",
          "AllowedPattern":"[\\x20-\\x7E]*",
          "ConstraintDescription":"can contain only ASCII characters."
        },
        "SSHLocation":{
          "Description":"The IP address range that can be used to SSH to the EC2 instances",
          "Type":"String",
          "MinLength":"9",
          "MaxLength":"18",
          "Default":"0.0.0.0/0",
          "AllowedPattern":"(\\d{1,3})\\.(\\d{1,3})\\.(\\d{1,3})\\.(\\d{1,3})/(\\d{1,2})",
          "ConstraintDescription":"must be a valid IP CIDR range of the form x.x.x.x/x."
        }
      },
      "Mappings":{
        "AWSInstanceType2Arch":{
          "t1.micro":{"Arch":"64"},
          "m1.small":{"Arch":"64"},
          "m1.medium":{"Arch":"64"},
          "m1.large":{"Arch":"64"},
          "m1.xlarge":{"Arch":"64"},
          "m2.xlarge":{"Arch":"64"},
          "m2.2xlarge":{"Arch":"64"},
          "m3.xlarge":{"Arch":"64"},
          "m3.2xlarge":{"Arch":"64"},
          "m2.4xlarge":{"Arch":"64"},
          "c1.medium":{"Arch":"64"},
          "c1.xlarge":{"Arch":"64"}
        },
        "AWSRegionArch2AMI":{
          "":{"32":"emi-ddbacddf","64":"emi-ddbacddf"}
        }
      },
      "Resources":{
        "ElasticLoadBalancer":{
          "Type":"AWS::ElasticLoadBalancing::LoadBalancer",
          "Properties":{
            "AvailabilityZones":{"Fn::GetAZs":""},
            "Instances":[{"Ref":"Ec2Instance1"},{"Ref":"Ec2Instance2"}],
            "Listeners"{"LoadBalancerPort":"80","InstancePort":{"Ref":"WebServerPort"},"Protocol":"HTTP"}],
            "HealthCheck":{
              "Target":{"Fn::Join":["",["HTTP:",{"Ref":"WebServerPort"},"/"]]},
              "HealthyThreshold":"3",
              "UnhealthyThreshold":"5",
              "Interval":"30",
              "Timeout":"5"
            }
          }
        },
        "Ec2Instance1":{
          "Type":"AWS::EC2::Instance",
          "Properties":{
            "SecurityGroups":[{"Ref":"InstanceSecurityGroup"}],
            "KeyName":{"Ref":"KeyName"},
            "InstanceType":{"Ref":"InstanceType"},
            "ImageId":{
              "Fn::FindInMap":[
                "AWSRegionArch2AMI",
                {"Ref":"AWS::Region"},
                {"Fn::FindInMap":["AWSInstanceType2Arch",{"Ref":"InstanceType"},"Arch"]}
              ]
            },
            "UserData":{"Fn::Base64":{"Ref":"WebServerPort"}}
          }
        },
        "Ec2Instance2":{
          "Type":"AWS::EC2::Instance",
          "Properties":{
            "SecurityGroups":[{"Ref":"InstanceSecurityGroup"}],
            "KeyName":{"Ref":"KeyName"},
            "InstanceType":{"Ref":"InstanceType"},
            "ImageId":{
              "Fn::FindInMap":[
                "AWSRegionArch2AMI",
                {"Ref":"AWS::Region"},
                {"Fn::FindInMap":["AWSInstanceType2Arch",{"Ref":"InstanceType"},"Arch"]}
              ]
            },
            "UserData":{"Fn::Base64":{"Ref":"WebServerPort"}}
          }
        },
        "InstanceSecurityGroup":{
          "Type":"AWS::EC2::SecurityGroup",
          "Properties":{
            "GroupDescription":"Enable SSH access and HTTP access on the inbound port",
            "SecurityGroupIngress":[
              {
                "IpProtocol":"tcp",
                "FromPort":"22",
                "ToPort":"22",
                "CidrIp":{"Ref":"SSHLocation"}
              },
              {
                 "IpProtocol":"tcp",
                 "FromPort":{"Ref":"WebServerPort"},
                 "ToPort":{"Ref":"WebServerPort"},
                 "CidrIp":"0.0.0.0/0"
              }
            ]
          }
        }
      },
      "Outputs":{
        "URL":{
          "Description":"URL of the sample website",
          "Value":{"Fn::Join":["",["http://",{"Fn::GetAtt":["ElasticLoadBalancer","DNSName"]}]]}
        }
      }
    }


## IAMGroup.template

    {
      "AWSTemplateFormatVersion":"2010-09-09",
      "Resources":{
        "Group1":{
          "Type":"AWS::IAM::Group",
          "Properties":{
            "Path":"/myapplication/",
            "Policies":[{
              "PolicyName":"myapppolicy",
              "PolicyDocument":{
                "Version":"2012-10-17",
                "Statement":[
                  {"Effect":"Allow","Action":["ec2:*"],"Resource":["*"]},
                  {"Effect":"Deny","Action":["s3:*"],"NotResource":["*"]}
                ]
              }
            }]
          }
        }
      },
      "Outputs":{
        "Group1Ref":{
          "Value":{"Ref":"Group1"}
        },
        "Group1Arn":{
          "Value":{"Fn::GetAtt":["Group1","Arn"]}
        }
      }
    }


## IAMRole.template

    {
      "AWSTemplateFormatVersion":"2010-09-09",
      "Resources":{
        "Role1":{
          "Type":"AWS::IAM::Role",
          "Properties":{
            "AssumeRolePolicyDocument":{
              "Version":"2012-10-17",
              "Statement":[{
                "Effect":"Allow",
                "Principal":{"Service":["ec2.amazonaws.com"]},
                "Action":["sts:AssumeRole"]
              }]
            },
            "Path":"/",
            "Policies":[{
              "PolicyName":"root",
              "PolicyDocument":{
                "Version":"2012-10-17",
                "Statement":[{"Effect":"Allow","Action":"*","Resource":"*"}]
              }
            }]
          }
        },
        "IP1":{
          "Type":"AWS::IAM::InstanceProfile",
          "Properties":{
            "Path":"/",
            "Roles":[{"Ref":"Role1"}]
          }
        }
      },
      "Outputs":{
        "Role1Ref":{
          "Value":{"Ref":"Role1"}
        },
        "Role1Arn":{
          "Value":{"Fn::GetAtt":["Role1","Arn"]}
        },
        "IP1Ref":{
          "Value":{"Ref":"IP1"}
        },
        "IP1Arn":{
          "Value":{"Fn::GetAtt":["IP1","Arn"]}
        }
      }
    }


## IAM_Users_Groups_and_Policies.template

    {
      "AWSTemplateFormatVersion":"2010-09-09",
      "Description":"AWS CloudFormation Sample Template IAM_Users_Groups_and_Policies: Sample template showing how to create IAM users, groups and policies. It creates a single user that is a member of a users group and an admin group. The groups each have different IAM policies associated with them. Note: This example also creates an AWSAccessKeyId/AWSSecretKey pair associated with the new user. The example is somewhat contrived since it creates all of the users and groups, typically you would be creating policies, users and/or groups that contain references to existing users or groups in your environment. Note that you will need to specify the CAPABILITY_IAM flag when you create the stack to allow this template to execute. You can do this through the AWS management console by clicking on the check box acknowledging that you understand this template creates IAM resources or by specifying the CAPABILITY_IAM flag to the cfn-create-stack command line tool or CreateStack API call. ",
      "Parameters":{
        "Password":{
          "NoEcho":"true",
          "Type":"String",
          "Description":"New account password",
          "MinLength":"1",
          "MaxLength":"41"
        }
      },
      "Resources":{
        "CFNUser":{
          "Type":"AWS::IAM::User",
          "Properties":{
            "LoginProfile":{"Password":{"Ref":"Password"}}
          }
        },
        "Role1":{
          "Type":"AWS::IAM::Role",
          "Properties":{
            "AssumeRolePolicyDocument":{
              "Version":"2012-10-17",
              "Statement":[{
                "Effect":"Allow",
                "Principal":{"Service":["ec2.amazonaws.com"]},
                "Action":["sts:AssumeRole"]
              }]
            },
            "Path":"/",
            "Policies":[{
              "PolicyName":"root",
              "PolicyDocument":{
                "Version":"2012-10-17",
                "Statement":[{"Effect":"Allow","Action":"*","Resource":"*"}]
              }
            }]
          }
        },
        "CFNUserGroup":{
          "Type":"AWS::IAM::Group"
        },
        "CFNAdminGroup":{
          "Type":"AWS::IAM::Group"
        },
        "Users":{
          "Type":"AWS::IAM::UserToGroupAddition",
          "Properties":{
            "GroupName":{"Ref":"CFNUserGroup"},
            "Users":[{"Ref":"CFNUser"}]
          }
        },
        "Admins":{
          "Type":"AWS::IAM::UserToGroupAddition",
          "Properties":{
            "GroupName":{"Ref":"CFNAdminGroup"},
            "Users":[{"Ref":"CFNUser"}]
          }
        },
        "CFNUserPolicies":{
          "Type":"AWS::IAM::Policy",
          "Properties":{
            "PolicyName":"CFNUsers",
            "PolicyDocument":{
              "Statement":[{
                "Effect":"Allow",
                "Action":["cloudformation:Describe*","cloudformation:List*","cloudformation:Get*"],
                "Resource":"*"
              }]
            },
            "Groups":[{"Ref":"CFNUserGroup"}],
            "Users":[{"Ref":"CFNUser"}],
            "Roles":[{"Ref":"Role1"}]
          }
        },
        "CFNAdminPolicies":{
          "Type":"AWS::IAM::Policy",
          "Properties":{
            "PolicyName":"CFNAdmins",
            "PolicyDocument":{
              "Statement":[{"Effect":"Allow","Action":"cloudformation:*","Resource":"*"}]
            },
            "Groups":[{"Ref":"CFNAdminGroup"}]
          }
        },
        "CFNKeys":{
          "Type":"AWS::IAM::AccessKey",
          "Properties":{
            "UserName":{"Ref":"CFNUser"}
          }
        }
      },
      "Outputs":{
        "AccessKey":{
          "Value":{"Ref":"CFNKeys"},
          "Description":"AWSAccessKeyId of new user"
        },
        "SecretKey":{
          "Value":{"Fn::GetAtt":["CFNKeys","SecretAccessKey"]},
          "Description":"AWSSecretKey of new user"
        }
      }
    }


## IAMUser.template

    {
      "AWSTemplateFormatVersion":"2010-09-09",
      "Parameters":{
        "Password":{
          "NoEcho":"true",
          "Type":"String",
          "Description":"New account password",
          "MinLength":"1",
          "MaxLength":"41"
        }
      },
      "Resources":{
        "CFNUserGroup":{
          "Type":"AWS::IAM::Group",
          "Properties":{
            "Policies":[{
              "PolicyName":"CFNUsers",
              "PolicyDocument":{
                "Statement":[{
                  "Effect":"Allow",
                  "Action":["cloudformation:Describe*","cloudformation:List*","cloudformation:Get*"],
                  "Resource":"*"
                }]
              }
            }]
          }
        },
        "CFNAdminGroup":{
          "Type":"AWS::IAM::Group"
        },
        "CFNUser":{
          "Type":"AWS::IAM::User",
          "Properties":{
            "LoginProfile":{"Password":{"Ref":"Password"}},
            "Groups":[{"Ref":"CFNUserGroup"},{"Ref":"CFNAdminGroup"}],
            "Policies":[{
              "PolicyName":"CFNUsers",
              "PolicyDocument":{
                "Statement":[{
                  "Effect":"Allow",
                  "Action":["cloudformation:Describe*","cloudformation:List*","cloudformation:Get*"],
                  "Resource":"*"
                }]
              }
            }]
          }
        }
      }
    }


## SecurityGroupRule.template

    {
    "AWSTemplateFormatVersion":"2010-09-09",
      "Description":"Create an EC2 instance running a specified EMI, a security group, and an ingress rule.",
      "Parameters":{
        "ImageId":{
          "Description":"Image id",
          "Type":"String"
        }
      },
      "Resources":{
        "Ec2Instance1":{
          "Description":"My instance",
          "Type":"AWS::EC2::Instance",
          "Properties":{
            "ImageId":{"Ref":"ImageId"}
          },
          "DependsOn":"Ec2Instance2"
        },
        "Ec2Instance2":{
          "Type":"AWS::EC2::Instance",
          "Properties":{
            "ImageId":{"Ref":"ImageId"},
            "SecurityGroups":[{"Ref":"InstanceSecurityGroup"}]
          }
        },
        "InstanceSecurityGroup":{
          "Type":"AWS::EC2::SecurityGroup",
          "Properties":{
            "GroupDescription":"Cloudformation Group",
            "SecurityGroupIngress":[{"IpProtocol":"tcp","FromPort":"22","ToPort":"22","CidrIp":"0.0.0.0/0"}]
          }
        },
        "IngressRule":{
          "Type":"AWS::EC2::SecurityGroupIngress",
          "Properties":{
            "GroupName":{"Ref":"InstanceSecurityGroup"},
            "FromPort":"80",
            "ToPort":"80",
            "IpProtocol":"tcp",
            "SourceSecurityGroupName":{"Ref":"InstanceSecurityGroup"}
          }
        }
      }
    }


## Volumes.template

    {
      "AWSTemplateFormatVersion":"2010-09-09",
      "Description":"Create an EC2 instance running a specified EMI and attached volumes.",
      "Parameters":{
        "ImageId":{
          "Description":"Image id",
          "Type":"String"
        }
      },
      "Resources":{
        "Volume1":{
          "Type":"AWS::EC2::Volume",
          "Properties":{
            "Size":"5",
            "AvailabilityZone":{"Fn::GetAtt":["Instance1","AvailabilityZone"]}
          }
        },
        "Volume2":{
          "Type":"AWS::EC2::Volume",
          "Properties":{
            "Size":"5",
            "AvailabilityZone":{"Fn::GetAtt":["Instance1","AvailabilityZone"]}
          }
        },
        "MountPoint1":{
          "Type":"AWS::EC2::VolumeAttachment",
          "Properties":{
            "InstanceId":{"Ref":"Instance1"},
            "VolumeId":{"Ref":"Volume1"},
            "Device":"/dev/sdc"
          }
        },
        "Instance1":{
          "Type":"AWS::EC2::Instance",
          "Properties":{
            "ImageId":{"Ref":"ImageId"}
          }
        },
        "Instance2":{
          "Type":"AWS::EC2::Instance",
          "Properties":{
            "ImageId":{"Ref":"ImageId"},
            "Volumes":[{"VolumeId":{"Ref":"Volume2"},"Device":"/dev/sdc"}]
          } 
        }
      }
    }

