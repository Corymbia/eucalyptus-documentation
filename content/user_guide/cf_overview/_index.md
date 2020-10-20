+++
title = "Using CloudFormation"
weight = 120
+++


This topic describes the Eucalyptus implementation of the AWS CloudFormation web service, how CloudFormation works, and some details and examples of how to add CloudFormation to your Eucalyptus deployment.

## Why use CloudFormation?
Cloud computing allows for application repeatability and redundancy. This means that you can spin up as many virtual machines as you need, but the application configuration only needs to happen when the images are created. CloudFormation takes this concept to the next level: it allows you to configure an entire set of resources (instances, security groups, user roles and policies, and more) in a single template. Then you can create a stack of all those resources from the template using a single command. So, you don't just get machine repeatability, you get environment repeatability. CloudFormation allows you to clone environments in different cloud setups, as well as giving applications the ability to be set up and torn down in a repeatable manner.


## How does CloudFormation Work?
CloudFormation manages a set of resources, called a stack, in batch operations (create, update, or delete). Stacks are described in templates, which can be simple, as the following example: 

```yaml
Resources:
  MyInstance:
    Type: AWS::EC2::Instance
    Properties:
      ImageId: emi-371ada125a928669e
```

This stack creates a single instance, based on the image with ID `emi-371ada125a928669e`. However, this stack is not portable because different clouds might have different image IDs. 

CloudFormation allows stack customization through user parameters that are passed in at stack creation time. The following is an example of the template above with a user parameter called *MyImageId*.


```yaml
Parameters:
  MyImageId:
    Description: Image id
    Type: String
Resources:
  MyInstance:
    Type: AWS::EC2::Instance
    Properties:
      ImageId: !Ref MyImageId
```    

This stack creates a single instance, but the image ID will be required to be passed in using the command line. For example, the following example uses the *euform-create-stack* command in Euca2ools: 

```bash
euform-create-stack --template-file template.yaml -p MyImageId=emi-371ada125a928669e MyStack
```

or using the AWS CLI:

```bash
aws cloudformation create-stack --template-body file://template.yaml --parameters ParameterKey=MyImageId,ParameterValue=emi-371ada125a928669e --stack-name MyStack
```

These example commands pass the parameter *MyImageId* with value `emi-371ada125a928669e` into the stack creation process. 

You can also use templates to create multiple resources and associate them with each other. For example, the following template creates an instance with its own security group and ingress rule.


```yaml
Parameters:
  MyImageId:
    Description: Image id
    Type: String
Resources:
  MySecurityGroup:
    Type: AWS::EC2::SecurityGroup
    Properties:
      GroupDescription: Security Group with Ingress Rule for MyInstance
      SecurityGroupIngress:
        - IpProtocol: tcp
          FromPort: '22'
          ToPort: '22'
          CidrIp: '0.0.0.0/0'
  MyInstance:
    Type: AWS::EC2::Instance
    Properties:
      ImageId: !Ref 'MyImageId'
      SecurityGroups:
        - !Ref 'MySecurityGroup'
```

Templates can be more complicated than the ones shown above, but CloudFormation allows many resources to be deployed in one operation. Resources from most Eucalyptus services are supported. 


## CloudFormation Requirements
To run CloudFormation on Eucalyptus, you need the following: 

* A running Eucalyptus cloud, version 4.0 or later, with at least one Cloud Controller, Node Controller, and Cluster Controller up, running and registered 
* At least one active running service of each of the following: CloudWatch, AutoScaling, Load Balancing, Compute, and IAM 
* A registered active CloudFormation service 

{{% notice note %}}
Eucalyptus versions earlier than 5 support JSON CloudFormation templates but not the newer YAML format
{{% /notice %}}

## Supported Resources
The following resources are supported by CloudFormation in Eucalyptus. 

| Resource | Description | 
|  :---- |  :---- | 
| AWS::AutoScaling::AutoScalingGroup | All properties in the Template Reference section of the AWS CloudFormation User Guide are supported except: HealthCheckType. | 
| AWS::AutoScaling::LaunchConfiguration | All properties in the Template Reference section of the AWS CloudFormation User Guide are supported except AssociatePublicIpAddress. | 
| AWS::AutoScaling::ScalingPolicy | All properties in the Template Reference section of the AWS CloudFormation User Guide are supported. | 
| AWS::CloudFormation::Stack | All properties in the Template Reference section of the AWS CloudFormation User Guide are supported. | 
| AWS::CloudFormation::WaitCondition | All properties in the Template Reference section of the AWS CloudFormation User Guide are supported. | 
| AWS::CloudFormation::WaitConditionHandle. | All properties in the Template Reference section of the AWS CloudFormation User Guide are supported. | 
| AWS::CloudWatch::Alarm | All properties in the Template Reference section of the AWS CloudFormation User Guide are supported. | 
| AWS::EC2::CustomerGateway | All properties in the Template Reference section of the AWS CloudFormation User Guide are supported. | 
| AWS::EC2::DHCPOptions | All properties in the Template Reference section of the AWS CloudFormation User Guide are supported. | 
| AWS::EC2::EIP | All properties in the Template Reference section of the AWS CloudFormation User Guide are supported. | 
| AWS::EC2::EIPAssociation | All properties in the Template Reference section of the AWS CloudFormation User Guide are supported except: PrivateIpAddress. | 
| AWS::EC2::Instance | All properties in the Template Reference section of the AWS CloudFormation User Guide are supported except: SourceDestCheck, Tags, and Tenancy. | 
| AWS::EC2::InternetGateway | All properties in the Template Reference section of the AWS CloudFormation User Guide are supported. | 
| AWS::EC2::LaunchTemplate | All properties in the Template Reference section of the AWS CloudFormation User Guide are supported. | 
| AWS::EC2::NatGateway | All properties in the Template Reference section of the AWS CloudFormation User Guide are supported. | 
| AWS::EC2::NetworkAcl | All properties in the Template Reference section of the AWS CloudFormation User Guide are supported. | 
| AWS::EC2::NetworkAclEntry | All properties in the Template Reference section of the AWS CloudFormation User Guide are supported. | 
| AWS::EC2::NetworkInterface | All properties in the Template Reference section of the AWS CloudFormation User Guide are supported. | 
| AWS::EC2::NetworkInterfaceAttachment | All properties in the Template Reference section of the AWS CloudFormation User Guide are supported. | 
| AWS::EC2::Route | All properties in the Template Reference section of the AWS CloudFormation User Guide are supported. | 
| AWS::EC2::RouteTable | All properties in the Template Reference section of the AWS CloudFormation User Guide are supported. | 
| AWS::EC2::SecurityGroup | All properties in the Template Reference section of the AWS CloudFormation User Guide are supported. | 
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
| AWS::IAM::ManagedPolicy | All properties in the Template Reference section of the AWS CloudFormation User Guide are supported. | 
| AWS::IAM::Policy | All properties in the Template Reference section of the AWS CloudFormation User Guide are supported. | 
| AWS::IAM::Role | All properties in the Template Reference section of the AWS CloudFormation User Guide are supported. | 
| AWS::IAM::User | All properties in the Template Reference section of the AWS CloudFormation User Guide are supported. | 
| AWS::IAM::UserToGroupAddition | All properties in the Template Reference section of the AWS CloudFormation User Guide are supported. | 
| AWS::Route53::HostedZone | All properties in the Template Reference section of the AWS CloudFormation User Guide are supported. | 
| AWS::Route53::RecordSet | All properties in the Template Reference section of the AWS CloudFormation User Guide are supported. | 
| AWS::Route53::RecordSetGroup | All properties in the Template Reference section of the AWS CloudFormation User Guide are supported. | 
| AWS::S3::Bucket | All properties in the Template Reference section of the AWS CloudFormation User Guide are supported. | 
| AWS::S3::BucketPolicy | All properties in the Template Reference section of the AWS CloudFormation User Guide are supported. | 
| AWS::SQS::Queue | All properties in the Template Reference section of the AWS CloudFormation User Guide are supported. | 
| AWS::SQS::QueuePolicy | All properties in the Template Reference section of the AWS CloudFormation User Guide are supported. | 


## CloudFormation Endpoint
The service endpoint for CloudFormation is of the form:

```
http://cloudformation.mycloud.example.com:8773/
```

If DNS is not availble for your cloud, then an endpoint with a service path can be used:

```
http://<host-ip>:8773/services/CloudFormation
```

CloudFormation follows the same convention as the other user facing services. 


{{% children sort="weight" %}}
