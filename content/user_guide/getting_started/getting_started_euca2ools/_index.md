+++
title = "Getting Started with Euca2ools"
weight = 20
+++


This section helps you get started using your Eucalyptus cloud, and covers setting up your user credentials, installing and configuring the command line tools, and working with images and instances.As a cloud user, you can access the Eucalyptus cloud using a command line interface such as Euca2ools, or using a web-based interface such as the Eucalyptus Management Console.


{{% notice note %}}
This section primarily deals with using the Eucalyptus command line. For complete documentation on using web-based the Eucalyptus Console, see [Console Login]({{< ref console_login.md >}}).
{{% /notice %}}

To access Eucalyptus via the command line tools, you need keys for Euca2ools. To access Eucalyptus with the Management Console, you'll need a password for the Management Console. Talk to your cloud administrator to get your keys and passwords.

## Find Image

Enter the following command:

```bash
# euca-describe-images -a
IMAGE	emi-0ba907069cb1845bc	ubuntu-focal/focal-server-cloudimg-amd64.raw.manifest.xml	000575948401	available	public	x86_64	machine				instance-storehvm	
IMAGE	emi-371ada125a928669e	centos-7/CentOS-7-x86_64-GenericCloud-2003.raw.manifest.xml	000575948401	available	public	x86_64	machine				instance-storehvm	
```

Look for the image ID in the second column and write it down. The image ID starts with `emi-` . Once you find a suitable image to use, make sure you have a keypair to use.

## Create KeyPairs

Enter the following command:

```bash
euca-create-keypair -f <keypair_name>.private <keypair_name>
```

where `<keypair_name>` is a unique name for your keypair. For example:

```bash
euca-create-keypair -f "alice-keypair.private" "alice-keypair"
```

The private key is saved to a file in your local directory. Query the system to view the public key:

```bash
# euca-describe-keypairs
KEYPAIR	alice-keypair	92:40:28:cb:08:54:80:95:8d:69:d9:ab:9a:ff:28:30:40:12:6a:66
```

## Authorize Security Groups

Before you can log in to an instance, you must authorize access to that instance. This done by configuring a security group for that instance.

A security group is a set of networking rules applied to instances associated with that group. When you first create an instance, it is assigned to a default security group that denies incoming network traffic from all sources. To allow login and usage of a new instance, you must authorize network access to the default security group with the euca-authorize command.

To authorize a security group, use euca-authorize with the name of the security group, and the options of the network rules you want to apply.

```bash
euca-authorize <security_group>
```

Use the following command to grant unlimited network access using SSH (TCP, port 22) and VNC (TCP, ports 5900 to 5910) to the security group `default` :

```bash
# euca-authorize -P tcp -p 22 -s 0.0.0.0/0 default
# euca-authorize -P tcp -p 5900-5910 -s 0.0.0.0/0 default
```
 
## Launch an Instance

Use the euca-run-instances command and provide an image ID and the user data file, in the format `euca-run-instances <image_id>` . For example: 

```bash
euca-run-instances emi-371ada125a928669e
```

For additional details and options that can be used with the *euca-run-instances* command. Enter the following command to get the launch status of the instance: 

```bash
euca-describe-instances <instance_id>
```

## Log in to an Instance

When you create an instance, Eucalyptus assigns the instance two IP addresses: a public IP address and a private IP address. The public IP address provides access to the instance from external network sources; the private IP address provides access to the instance from within the Eucalyptus cloud environment. For more information on Eucalyptus networking modes, see the [Eucalyptus Administrator’s Guide]({{< ref admin_guide >}}).

To use an instance you must log into it via ssh using one of the IP addresses assigned to it. You can obtain the instance’s IP addresses using the euca-describe-instances query as shown in the following example.

To log into a VM instance:

Enter the following command to view the IP addresses of your instance:

```bash
# euca-describe-instances
RESERVATION	r-825a2c9c04e97ee62	000332850814	default
INSTANCE	i-131e5853a71c87f16	emi-371ada125a928669e	euca-192-168-134-74.eucalyptus.mycloud.example.com	euca-172-31-15-2.eucalyptus.internal	running		0		t2.micro	2020-10-19T16:35:36.120Z	cloud-1a				monitoring-disabled	192.168.134.74	172.31.15.2	vpc-bded94e5dd0a07bc3	subnet-1343e38b5566c8e90	instance-store					hvm			sg-84741faf0bd87ea73				x86_64
NETWORKINTERFACE	eni-c1ba7d641cb70a7ee	subnet-1343e38b5566c8e90	vpc-bded94e5dd0a07bc3	000332850814	in-use	172.31.15.2	euca-172-31-15-2.eucalyptus.internal	true
ATTACHMENT		eni-attach-d597b44874e84bbb2	0	attached	2020-10-19T16:35:36.125Z	true
ASSOCIATION	192.168.134.74		172.31.15.2
GROUP	sg-84741faf0bd87ea73	default
PRIVATEIPADDRESS	172.31.15.2	euca-172-31-15-2.eucalyptus.internal	primary
```

Note that the public IP address appears after the *monitoring-disabled* text, with the private address immediately following.

Look for the instance ID in the second field of the *INSTANCE* line and write it down. Use this ID to manipulate and terminate this instance.

{{% notice note %}}
Be sure that the security group for the instance allows SSH access.
{{% /notice %}}

Use SSH to log into the instance, using your private key and the public IP address. For example:

```bash
ssh -i alice-keypair.private root@192.168.134.74 
```

You are now logged in to your Linux instance. 

## Terminate an Instance

The *euca-terminate-instances* command lets you cancel running VM instances. When you terminate instances, you must specify the ID string of the instance(s) you wish to terminate. You can obtain the ID strings of your instances using the *euca-describe-instances* or *euca-describe-instance-status* commands. 


{{% notice warning %}}
Terminating an instance can cause the instance and all items associated with the instance (data, packages installed, etc.) to be lost. Be sure to save any important work or data to Object Storage or EBS before terminating an instance. 
{{% /notice %}}

To terminate VM instances: 

Enter *euca-describe-instance-status* to obtain the ID of the instances you wish to terminate. Note that an instance ID strings begin with the prefix `i-`: 

```bash
# euca-describe-instance-status
INSTANCE	i-131e5853a71c87f16	cloud-1a	running	16	ok	ok	active	
SYSTEMSTATUS	reachability	passed	
INSTANCESTATUS	reachability	passed
```

Enter *euca-terminate-instances* and the ID string(s) of the instance(s) you wish to terminate: 

```bash
# euca-terminate-instances i-131e5853a71c87f16
INSTANCE	i-131e5853a71c87f16	running	shutting-down
```
