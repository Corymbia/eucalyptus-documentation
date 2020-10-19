+++
title = "Getting Started with the AWS CLI"
weight = 15
+++

This section helps you get started using your Eucalyptus cloud, and covers setting up your user credentials, installing and configuring the AWS CLI, and working with images and instances. As a cloud user, you can access the Eucalyptus cloud using a command line interface such as the AWS CLI, or using a web-based interface such as the Eucalyptus Management Console.

{{% notice note %}}
This section primarily deals with using the AWS CLI. For complete documentation on using web-based the Eucalyptus Console, see [Console Login]({{< ref console_login.md >}}). 
{{% /notice %}}

The install guide covers ["AWS CLI Installation"]({{< ref installing_awscli >}})

## Find Image

Enter the following command: 

```bash
# aws ec2 describe-images
IMAGES	x86_64	2020-10-17T05:29:09.161Z	emi-0ba907069cb1845bc	ubuntu-focal/focal-server-cloudimg-amd64.raw.manifest.xml	machine	ubuntu-focal	000575948401		True	/dev/sda	instance-store	available	hvm
IMAGES	x86_64	2020-10-17T05:24:08.857Z	emi-371ada125a928669e	centos-7/CentOS-7-x86_64-GenericCloud-2003.raw.manifest.xml	machine	centos-7	000575948401		True	/dev/sda	instance-store	available	hvm
```

Look for the image ID and write it down. The image ID starts with `emi-` . Once you find a suitable image to use, make sure you have a keypair to use. 

{{% notice note %}}
Examples use the AWS CLI *text* output format. You can request this output for a command by adding an "--output text" argument to any command.
{{% /notice %}}

## Create KeyPairs

Enter the following command: 

```bash
aws ec2 create-key-pair --key-name <keypair_name> > <keypair_name>.private
```

where `<keypair_name>` is a unique name for your keypair. For example: 

```bash
aws ec2 create-key-pair --key-name "alice-keypair" > "alice-keypair.private"
```

The private key is saved to a file in your local directory. Query the system to view the public key: 

```bash
# aws ec2 describe-key-pairs
KEYPAIRS	92:40:28:cb:08:54:80:95:8d:69:d9:ab:9a:ff:28:30:40:12:6a:66	alice-keypair
```

## Authorize Security Groups

Before you can log in to an instance, you must authorize access to that instance. This done by configuring a security group for that instance. 

A security group is a set of networking rules applied to instances associated with that group. When you first create an instance, it is assigned to a default security group that denies incoming network traffic from all sources. To allow login and usage of a new instance, you must authorize network access to the default security group with the authorize-security-group-ingress command. 

To authorize a security group, use authorize-security-group-ingress with the name of the security group, and the options of the network rule permissions you want to apply.

```bash
aws ec2 authorize-security-group-ingress [--group-id <value>] [--group-name <value>] [--ip-permissions <value>]
```

Use the following command to grant unlimited network access using SSH (TCP, port 22) and VNC (TCP, ports 5900 to 5910) to the security group `default` : 

```bash
# aws ec2 authorize-security-group-ingress --ip-permissions "IpProtocol=tcp,FromPort=22,ToPort=22,IpRanges={CidrIp=0.0.0.0/0}" --group-name default 
# aws ec2 authorize-security-group-ingress --ip-permissions "IpProtocol=tcp,FromPort=5900,ToPort=5910,IpRanges={CidrIp=0.0.0.0/0}" --group-name default 
```

## Launch an Instance

Use the run-instances command and provide an image ID. For example:

```bash
aws ec2 run-instances --image-id emi-371ada125a928669e
```

For additional details and options that can be used with the run-instances command. Enter the following command to get the launch status of the instance: 

```bash
aws ec2 describe-instances --instance-ids <instance_id>
```

## Log in to an Instance

When you create an instance, Eucalyptus assigns the instance two IP addresses: a public IP address and a private IP address. The public IP address provides access to the instance from external network sources; the private IP address provides access to the instance from within the Eucalyptus cloud environment. For more information on Eucalyptus networking modes, see the [Eucalyptus Administrator’s Guide]({{< ref admin_guide >}}).

To use an instance you must log into it via ssh using one of the IP addresses assigned to it. You can obtain the instance’s IP addresses using the describe-instances query as shown in the following example.

To log into a VM instance:

Enter the following command to view the IP addresses of your instance:

```bash
# aws ec2 describe-instances
RESERVATIONS	000332850814	r-825a2c9c04e97ee62
GROUPS	sg-84741faf0bd87ea73	default
INSTANCES	0	x86_64	emi-371ada125a928669e	i-131e5853a71c87f16	t2.micro	2020-10-19T16:35:36.120Z	euca-172-31-15-2.eucalyptus.internal	172.31.15.2	euca-192-168-134-74.eucalyptus.mycloud.example.com	192.168.134.74	/dev/sda1	instance-store	True	NORMAL:  -- []	subnet-1343e38b5566c8e90	hvm	vpc-bded94e5dd0a07bc3
MONITORING	disabled
NETWORKINTERFACES	Primary network interface	d0:0d:c1:ba:7d:64	eni-c1ba7d641cb70a7ee	000332850814	euca-172-31-15-2.eucalyptus.internal	172.31.15.2	True	in-usesubnet-1343e38b5566c8e90	vpc-bded94e5dd0a07bc3
ASSOCIATION	euca-192-168-134-74.eucalyptus.mycloud.example.com	192.168.134.74
ATTACHMENT	2020-10-19T16:35:36.125Z	eni-attach-d597b44874e84bbb2	True	0	attached
GROUPS	sg-84741faf0bd87ea73	default
PRIVATEIPADDRESSES	True	euca-172-31-15-2.eucalyptus.internal	172.31.15.2
ASSOCIATION	euca-192-168-134-74.eucalyptus.mycloud.example.com	192.168.134.74
PLACEMENT	cloud-1a
SECURITYGROUPS	sg-84741faf0bd87ea73	default
STATE	16	running
```

Note that the public IP address is on the *INSTANCES* line after "mycloud.example.com", the private address is after "eucalyptus.internal".

Look for the instance ID on the *INSTANCE* line and write it down. Use this ID to manipulate and terminate this instance.

{{% notice note %}}
Be sure that the security group for the instance allows SSH access.
{{% /notice %}}

Use SSH to log into the instance, using your private key and the public IP address. For example:

```bash
ssh -i alice-keypair.private root@192.168.134.74 
```

You are now logged in to your Linux instance. 

## Terminate an Instance

The terminate-instances command lets you cancel running VM instances. When you terminate instances, you must specify the ID string of the instance(s) you wish to terminate. You can obtain the ID strings of your instances using the describe-instances or describe-instance-status commands. 


{{% notice warning %}}
Terminating an instance can cause the instance and all items associated with the instance (data, packages installed, etc.) to be lost. Be sure to save any important work or data to Object Storage or EBS before terminating an instance. 
{{% /notice %}}

To terminate VM instances: 

Enter describe-instance-status to obtain the ID of the instances you wish to terminate. Note that an instance ID strings begin with the prefix `i-` followed by an 8-character string: 

```bash
# aws ec2 describe-instance-status 
INSTANCESTATUSES	cloud-1a	i-131e5853a71c87f16
INSTANCESTATE	16	running
INSTANCESTATUS	ok
DETAILS	reachability	passed
SYSTEMSTATUS	ok
DETAILS	reachability	passed
```

Enter terminate-instances and the ID string(s) of the instance(s) you wish to terminate: 

```bash
# aws ec2 terminate-instances --instance-ids i-131e5853a71c87f16
TERMINATINGINSTANCES	i-131e5853a71c87f16
CURRENTSTATE	32	shutting-down
PREVIOUSSTATE	16	running
```


