+++
title = "Log in to an Instance"
weight = 50
+++


## For a Linux Instance
When you create an instance, Eucalyptus assigns the instance two IP addresses: a public IP address and a private IP address. The public IP address provides access to the instance from external network sources; the private IP address provides access to the instance from within the Eucalyptus cloud environment. Note that the two IP addresses may be the same depending on the current networking mode set by the administrator. For more information on Eucalyptus networking modes, see the Eucalyptus Administrator’s Guide. 

To use an instance you must log into it via ssh using one of the IP addresses assigned to it. You can obtain the instance’s IP addresses using the euca-describe-instances query as shown in the following example. 

To log into a VM instance: 

Enter the following command to view the IP addresses of your instance: 

    euca-describe-instances

Eucalyptus returns output similar to the following: 

    RESERVATION	r-338206B5	alice	default
    INSTANCE	i-4DCF092C  emi-EC1410C1  192.168.7.24	  10.17.0.130 ↵ running 	alice-keypair 	0 	m1.small  2010-03-15T21:57:45.134Z

Note that the public IP address appears after the image name, with the private address immediately following. 

Look for the instance ID in the second field and write it down. Use this ID to manipulate and terminate this instance. 
{{% notice note %}}
Be sure that the security group for the instance allows SSH access. For more information, see 
{{% /notice %}}
Use SSH to log into the instance, using your private key and the external IP address. For example: 

    ssh -i alice-keypair.private root@192.168.7.24 

You are now logged in to your Linux instance. 
## Using SSH to Connect via PuTTY
If you are a Windows user and want to securely connect to instances via PuTTY, you must first have a key pair.If you don't have a key pair, you can create one through the Management Console or the command line. For the key pair to be used with PuTTY, convert your .pem file to a .ppk file by performing the last step in the [Creating SSH Credentials for the Master Node: Modify Your PEM File](http://docs.aws.amazon.com/emr/latest/ManagementGuide/emr-plan-access-ssh.html) procedure. 
