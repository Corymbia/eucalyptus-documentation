+++
title = "CloudFormation Use Case"
weight = 20
+++

This topic describes a use case for creating a stack, checking the stack progress, and deleting the stack. For this use case, we will use the following template: 

```yaml
Parameters:
  MyImageId:
    Description: Image id
    Type: String
  MyKeyPair:
    Description: Key Pair
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
      KeyName: !Ref 'MyKeyPair'

```

This template creates an instance with a security group that allows global SSH access (port 22), but uses a keypair to log in. It requires two parameters, *MyImageId* , which is the image ID of the instance to create, and *MyKeyPair* , which is the name of the keypair to use to log in with. You could use both values with the *euca-run-instances* or *aws ec2 run-instances* commands to create an instance manually (for example, `euca-run-instances -k mykey emi-371ada125a928669e` ) so the arguments needed here are standard instance arguments. 

The steps to run this template through the system are explained in the following steps. 

{{% notice note %}}
These steps require that you have an available image and that the CloudFormation service is running 
{{% /notice %}}

Verify connectivity to the CloudFormation service. 

```bash
euform-describe-stacks 
# Or
aws cloudformation describe-stacks
```

You should not see anything returned, including any errors. Create a file called *ex_template.yaml* that contains the YAML template content shown in the introduction above.

Create a keypair. 

```bash
euca-create-keypair myKey > myKey.pem
# Or
aws ec2 create-key-pair --key-name myKey > myKey.pem
```

Set the permissions on the keypair. 

```bash
chmod 0600 myKey.pem
```

Find what resources have been created., run the command and the euca-describe-groups commands. Make note of the output for later. Run: 

```bash
euca-describe-images -a
# Or
aws ec2 describe-images
```

Note the output for later use.

Create the stack referencing the existing resources.

```bash
# euform-create-stack --template-file ex_template.yaml -p MyImageId=<image_id> -p MyKeyPair=myKey MyStack
arn:aws:cloudformation::000575948401:stack/MyStack/26daf046-3776-4b97-9444-5edae2f2eceb
```

of with the AWS CLI:

```bash
# aws cloudformation create-stack --template-body file://ex_template.yaml --parameters ParameterKey=MyImageId,ParameterValue=emi-371ada125a928669e ParameterKey=MyKeyPair,ParameterValue=myKey --stack-name MyStack
arn:aws:cloudformation::000575948401:stack/MyStack/26daf046-3776-4b97-9444-5edae2f2eceb
```

Run the checks you want on your stack. Check the status of the stack. 

```bash
# euform-describe-stacks
STACK	MyStack	CREATE_COMPLETE			2020-10-20T18:31:15.662Z
PARAMETER	MyImageId		emi-371ada125a928669e
PARAMETER	MyKeyPair		myKey
#
# aws cloudformation describe-stacks
STACKS	2020-10-20T18:31:15.662Z	False	2020-10-20T18:31:51.316Z	arn:aws:cloudformation::000575948401:stack/MyStack/26daf046-3776-4b97-9444-5edae2f2eceb	MyStack	CREATE_COMPLETE	
PARAMETERS	MyImageId	emi-371ada125a928669e
PARAMETERS	MyKeyPair	myKey
```

Check the stack at any time to see all the events that have occurred during the stack lifecycle. 

```bash
# euform-describe-stack-events MyStack
EVENT	MyStack	d87c4381-b765-4d44-a5ba-a952855ffd79	AWS::CloudFormation::Stack	MyStack	arn:aws:cloudformation::000575948401:stack/MyStack/26daf046-3776-4b97-9444-5edae2f2eceb	2020-10-20T18:31:51.310Z	CREATE_COMPLETE	
EVENT	MyStack	MyInstance-CREATE_COMPLETE-1603218711063	AWS::EC2::Instance	MyInstance	i-687f112f4c99e9a98	2020-10-20T18:31:51.063Z	CREATE_COMPLETE	
EVENT	MyStack	MyInstance-CREATE_IN_PROGRESS-1603218676951	AWS::EC2::Instance	MyInstance	i-687f112f4c99e9a98	2020-10-20T18:31:16.951Z	CREATE_IN_PROGRESS	Resource creation Initiated
EVENT	MyStack	MyInstance-CREATE_IN_PROGRESS-1603218676783	AWS::EC2::Instance	MyInstance		2020-10-20T18:31:16.783Z	CREATE_IN_PROGRESS	
EVENT	MyStack	MySecurityGroup-CREATE_COMPLETE-1603218676599	AWS::EC2::SecurityGroup	MySecurityGroup	MyStack-MySecurityGroup-SWUBTU8TQ9MBV	2020-10-20T18:31:16.599Z	CREATE_COMPLETE	
EVENT	MyStack	MySecurityGroup-CREATE_IN_PROGRESS-1603218676174	AWS::EC2::SecurityGroup	MySecurityGroup	MyStack-MySecurityGroup-SWUBTU8TQ9MBV	2020-10-20T18:31:16.174Z	CREATE_IN_PROGRESS	Resource creation Initiated
EVENT	MyStack	MySecurityGroup-CREATE_IN_PROGRESS-1603218676038	AWS::EC2::SecurityGroup	MySecurityGroup		2020-10-20T18:31:16.038Z	CREATE_IN_PROGRESS	
EVENT	MyStack	9212e1ff-6c7a-4710-96a2-d83606a3c34f	AWS::CloudFormation::Stack	MyStack	arn:aws:cloudformation::000575948401:stack/MyStack/26daf046-3776-4b97-9444-5edae2f2eceb	2020-10-20T18:31:15.780Z	CREATE_IN_PROGRESS	User Initiated
```

Run *euca-describe-instances* and *euca-describe-groups* to see the newly created resources:

```bash
# euca-describe-instances i-687f112f4c99e9a98
RESERVATION	r-2381c3e652dd942f2	000575948401	MyStack-MySecurityGroup-SWUBTU8TQ9MBV
INSTANCE	i-687f112f4c99e9a98	emi-371ada125a928669e	euca-192-168-134-181.eucalyptus.mycloud.example.com	euca-172-31-15-210.eucalyptus.internal	running	myKey	0		t2.micro	2020-10-20T18:31:16.920Z	cloud-1a				monitoring-disabled	192.168.134.181	172.31.15.210	vpc-837bc081de161f8c0	subnet-1503566df094fe78a	instance-store					hvm			sg-98da12246d91375e3				x86_64
NETWORKINTERFACE	eni-42a4a3bf7d1075735	subnet-1503566df094fe78a	vpc-837bc081de161f8c0	000575948401	in-use	172.31.15.210	euca-172-31-15-210.eucalyptus.internal	true
ATTACHMENT		eni-attach-cc38f4f4ef78a6469	0	attached	2020-10-20T18:31:16.923Z	true
ASSOCIATION	192.168.134.181		172.31.15.210
GROUP	sg-98da12246d91375e3	MyStack-MySecurityGroup-SWUBTU8TQ9MBV
PRIVATEIPADDRESS	172.31.15.210	euca-172-31-15-210.eucalyptus.internal	primary
TAG	instance	i-687f112f4c99e9a98	aws:cloudformation:logical-id	MyInstance
TAG	instance	i-687f112f4c99e9a98	aws:cloudformation:stack-id	arn:aws:cloudformation::000575948401:stack/MyStack/26daf046-3776-4b97-9444-5edae2f2eceb
TAG	instance	i-687f112f4c99e9a98	aws:cloudformation:stack-name	MyStack
TAG	instance	i-687f112f4c99e9a98	euca:node	10.117.111.18
#
# euca-describe-groups sg-98da12246d91375e3
GROUP	sg-98da12246d91375e3	000575948401	MyStack-MySecurityGroup-SWUBTU8TQ9MBV	Security Group with Ingress Rule for MyInstance	vpc-837bc081de161f8c0
PERMISSION	000575948401	MyStack-MySecurityGroup-SWUBTU8TQ9MBV	ALLOWS	tcp	22	22	FROM	CIDR	0.0.0.0/0	ingress
PERMISSION	000575948401	MyStack-MySecurityGroup-SWUBTU8TQ9MBV	ALLOWS	-1			TO	CIDR	0.0.0.0/0	egress
TAG	security-group	sg-98da12246d91375e3	aws:cloudformation:logical-id	MySecurityGroup
TAG	security-group	sg-98da12246d91375e3	aws:cloudformation:stack-id	arn:aws:cloudformation::000575948401:stack/MyStack/26daf046-3776-4b97-9444-5edae2f2eceb
TAG	security-group	sg-98da12246d91375e3	aws:cloudformation:stack-name	MyStack

```

To SSH into the instance:

```bash
ssh -i myKey.pem root@192.168.134.181
```

{{% notice note %}}
Username might depend on the image, and might be root, centos, ubuntu or ec2-user.
{{% /notice %}}

Delete the stack. 

```bash
euform-delete-stack MyStack
# Or
aws cloudformation delete-stack --stack-name MyStack
```

You can run *euform-describe-stacks* and all the other describe commands to check the progress until the delete is complete.

