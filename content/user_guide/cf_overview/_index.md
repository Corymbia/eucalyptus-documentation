+++
title = "Using CloudFormation"
weight = 120
chapter = true
+++


# Using CloudFormation
This topic describes the Eucalyptus implementation of the AWS CloudFormation web service, how CloudFormation works, and some details and examples of how to add CloudFormation to your Eucalyptus deployment.
## Why use CloudFormation?
Cloud computing allows for application repeatability and redundancy. This means that you can spin up as many virtual machines as you need, but the application configuration only needs to happen when the images are created. CloudFormation takes this concept to the next level: it allows you to configure an entire set of resources (instances, security groups, user roles and policies, and more) in a single JSON template file. Then you can run all with a single command. So, you don't just get machine repeatability, you get environment repeatability. CloudFormation allows you to clone environments in different cloud setups, as well as giving applications the ability to be set up and torn down in a repeatable manner. 


## How does CloudFormation Work?
CloudFormation manages a set of resources, called a stack, in batch operations (create, update, or delete). Stacks are described in JSON templates, and can be simple, as the following example: 



    {
      "Resources" : {
        "MyInstance": {
          "Type": "AWS::EC2::Instance",
          "Properties": {
            "ImageId" : "emi-db0b2276"
          }
        }
      }
    }

This stack creates a single instance, based on the image with ID `emi-db0b2276` . However, this stack is not portable because different clouds might have different image IDs. 

CloudFormation allows stack customization through user parameters that are passed in at stack creation time. The following is an example of the template above with a user parameter called `MyImageId` . Changes are in bold. 



    {
      "Parameters": {
        "MyImageId": {
          "Description":"Image id",
          "Type":"String"
        }
      },
      "Resources" : {
        "MyInstance": {
          "Type": "AWS::EC2::Instance",
          "Properties": {
            "ImageId" : { "Ref" : "MyImageId" }
          }
        }
      }
    }

This stack creates a single instance, but the image ID will be required to be passed in using the command line. For example, the following example uses the `euform-create-stack` command in Euca2ools: 



    euform-create-stack --template-file template.json -p MyImageId=emi-db0b2276 MyStack

This command passes the parameter `MyImageId` with value `emi-db0b2276` into the stack creation process using the `-p` flag. 

You can also use templates to create multiple resources and associate them with each other. For example, the following template creates an instance with its own security group and ingress rule. Additions are in bold. 



    {
      "Parameters": {
        "MyImageId": {
          "Description":"Image id",
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
            ]
          }
        }
      }
    }

Templates can be more complicated than the ones shown above, but CloudFormation allows many resources to be deployed in one operation. Resources from most Eucalyptus services are supported. 


## CloudFormation Requirements
To run CloudFormation on Eucalyptus, you need the following: 



* A running Eucalyptus cloud, version 4.0 or later, with at least one Cloud Controller, Node Controller, and Cluster Controller up, running and registered 
* At least one active running service of each of the following: CloudWatch, AutoScaling, Load Balancing, Compute, and IAM 
* A registered active CloudFormation service 

## Supported Resources
The following resources are supported by CloudFormation in Eucalyptus. 



| Resource | Description | 
|  :---- |  :---- | 
| AWS::AutoScaling::AutoScalingGroup | All properties in the Template Reference section of the AWS CloudFormation User Guide are supported except: HealthCheckType, Tags, and VpcZoneIdentifier. | 
| AWS::AutoScaling::LaunchConfiguration | All properties in the Template Reference section of the AWS CloudFormation User Guide are supported except AssociatePublicIpAddress. | 
| AWS::AutoScaling::ScalingPolicy | All properties in the Template Reference section of the AWS CloudFormation User Guide are supported. | 
| AWS::CloudFormation::WaitCondition | All properties in the Template Reference section of the AWS CloudFormation User Guide are supported. | 
| AWS::CloudFormation::WaitConditionHandle. | All properties in the Template Reference section of the AWS CloudFormation User Guide are supported. | 
| AWS::CloudWatch::Alarm | All properties in the Template Reference section of the AWS CloudFormation User Guide are supported. | 
| AWS::EC2::CustomerGateway | All properties in the Template Reference section of the AWS CloudFormation User Guide are supported. | 
| AWS::EC2::DHCPOptions | All properties in the Template Reference section of the AWS CloudFormation User Guide are supported. | 
| AWS::EC2::EIP | All properties in the Template Reference section of the AWS CloudFormation User Guide are supported except Domain. | 
| AWS::EC2::EIPAssociation | All properties in the Template Reference section of the AWS CloudFormation User Guide are supported except: AllocationId, NetworkInterfaceId, and PrivateIpAddress. | 
| AWS::EC2::Instance | All properties in the Template Reference section of the AWS CloudFormation User Guide are supported except: NetworkInterfaces, SecurityGroupIds, SourceDestCheck, Tags, and Tenancy. All other properties are forwarded to the Compute service internally but VPC is not implemented so VPC oriented properties are likely ignored there. | 
| AWS::EC2::InternetGateway | All properties in the Template Reference section of the AWS CloudFormation User Guide are supported. | 
| AWS::EC2::NetworkAcl | All properties in the Template Reference section of the AWS CloudFormation User Guide are supported. | 
| AWS::EC2::NetworkAclEntry | All properties in the Template Reference section of the AWS CloudFormation User Guide are supported. | 
| AWS::EC2::NetworkInterface | All properties in the Template Reference section of the AWS CloudFormation User Guide are supported. | 
| AWS::EC2::Route | All properties in the Template Reference section of the AWS CloudFormation User Guide are supported. | 
| AWS::EC2::RouteTable | All properties in the Template Reference section of the AWS CloudFormation User Guide are supported. | 
| AWS::EC2::SecurityGroup | All properties in the Template Reference section of the AWS CloudFormation User Guide are supported except: SecurityGroupEgress, Tags, and VpcId. | 
| AWS::EC2::SecurityGroupEgress | All properties in the Template Reference section of the AWS CloudFormation User Guide are supported. | 
| AWS::EC2::SecurityGroupIngress | All properties in the Template Reference section of the AWS CloudFormation User Guide are supported except SourceSecurityGroupId. | 
| AWS::EC2::Subnet | All properties in the Template Reference section of the AWS CloudFormation User Guide are supported. | 
| AWS::EC2::SubnetNetworkAclAssociation | All properties in the Template Reference section of the AWS CloudFormation User Guide are supported. | 
| AWS::EC2::SubnetRouteTableAssociation | All properties in the Template Reference section of the AWS CloudFormation User Guide are supported. | 
| AWS::EC2::Volume | All properties in the Template Reference section of the AWS CloudFormation User Guide are supported except: HealthCheckType and Tags. | 
| AWS::EC2::VolumeAttachment | All properties in the Template Reference section of the AWS CloudFormation User Guide are supported. | 
| AWS::EC2::VPC | All properties in the Template Reference section of the AWS CloudFormation User Guide are supported. | 
| AWS::EC2::VPCDHCPOptionsAssociation | All properties in the Template Reference section of the AWS CloudFormation User Guide are supported. | 
| AWS::EC2::VPCGatewayAttachment | All properties in the Template Reference section of the AWS CloudFormation User Guide are supported. | 
| AWS::ElasticLoadBalancing::LoadBalancer | All properties in the Template Reference section of the AWS CloudFormation User Guide are supported except: AccessLoggingPolicy, ConnectionDrainingPolicy, CrossZone, Policies.InstancePorts, and Policies.LoadBalanerPorts. All other properties are passed through to the LoadBalancing service internally but some features are not implemented so properties may be ignored there. | 
| AWS::IAM::AccessKey | All properties in the Template Reference section of the AWS CloudFormation User Guide are supported except Serial. | 
| AWS::IAM::Group | All properties in the Template Reference section of the AWS CloudFormation User Guide are supported. | 
| AWS::IAM::InstanceProfile | All properties in the Template Reference section of the AWS CloudFormation User Guide are supported. | 
| AWS::IAM::Policy | All properties in the Template Reference section of the AWS CloudFormation User Guide are supported. | 
| AWS::IAM::Role | All properties in the Template Reference section of the AWS CloudFormation User Guide are supported. | 
| AWS::IAM::User | All properties in the Template Reference section of the AWS CloudFormation User Guide are supported. | 
| AWS::IAM::UserToGroupAddition | All properties in the Template Reference section of the AWS CloudFormation User Guide are supported. | 
| AWS::S3::Bucket | All properties in the Template Reference section of the AWS CloudFormation User Guide are supported. | 


## CloudFormation Registration
To register CloudFormation for your cloud, enter the following command: 



    euserv-register-service -t CloudFormation -h CLOUD_FORMATION_HOST_IP SVCINSTANCE

For example: 



    euserv-register-service -t CloudFormation -h 203.0.113.13 cfn

Eucalyptus returns information similar to the following: 



    Created new partition 'cfn'
     SERVICE    cloudformation   	 cfn  		 cfn http://203.0.113.13:8773/services/
     CloudFormation    arn:euca:bootstrap:cfn:cloudformation:cfn/

The CloudFormation service will be shown when you run `euserv-describe-services` . 


## WSDL URL
The service WSDL URL for CloudFormation is of the form: 



    http://<host-ip>:8773/services/CloudFormation

The services path may not be necessary if DNS is enabled, it may look something like this: 



    http://cloudformation.g-19-10.autoqa.qa1.eucalyptus-systems.com:8773/

CloudFormation follows the same convention as the other user facing services. 



{{% children sort="weight" %}}
