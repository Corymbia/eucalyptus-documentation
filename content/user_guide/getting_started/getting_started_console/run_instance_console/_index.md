+++
title = "Launch and Connect to an Instance with the Management Console"
weight = 5
+++

To launch an instance: 

Click on the Launch Instance button on the main console page: 
![image]({{< ref "/" >}}images/run_instance_console_1.jpg)
Select an image from the list (for this example, we'll select a CentOS image), then click the Next button: 
![image]({{< ref "/" >}}images/run_instance_console_2.jpg)
Select an instance type and availability zone from the Details tab. For this example, select the defaults, and then click the Next button: 
![image]({{< ref "/" >}}images/run_instance_console_3.jpg)
On the Security tab, we'll create a key pair and a security group to use with our new instance. A key pair will allow you to access your instance, and a security group allows you to define what kinds of incoming traffic your instance will allow. 
![image]({{< ref "/" >}}images/run_instance_console_4.jpg)
First, we will create a key pair. Click the Create key pair link to bring up the Create key pair dialog: 
![image]({{< ref "/" >}}images/run_instance_console_4a.jpg)
Type the name of your new key pair into the Name text box, and then click the Create and Download button: 
![image]({{< ref "/" >}}images/run_instance_console_4b.jpg)
The key pair automatically downloads to a location on your computer, typically in the *Downloads* folder. The Create key pair dialog will close, and the Key name text box will be populated with the name of the key pair you just created: 
![image]({{< ref "/" >}}images/run_instance_console_4d.jpg)
Next, we will create a security group. Click the Create security group link to bring up the Create security group dialog: 
![image]({{< ref "/" >}}images/run_instance_console_4e.jpg)
On the Create security group dialog, type the name of your security group into the Name text box. Type a brief description of your security group into the Description text box. We'll need to SSH into our instance later, so in the Rules section of the dialog, select the SSH protocol from the Protocol drop-down list box. 
{{% notice note %}}
In this example, we allow any IP address to access our new instance. For production use, please use appropriate caution when specifying an IP range. For more information on CIDR notation, go to . 
{{% /notice %}}
You need to specify an IP address or a range of IP addresses that can use SSH to access your instance. For this example, click the Open to all addresses link. This will populate the IP Address text box with 0.0.0.0/0, which allows any IP address to access your instance via SSH. 
![image]({{< ref "/" >}}images/run_instance_console_4f.jpg)
Click the Add rule button. The Create security group dialog should now look something like this: 
![image]({{< ref "/" >}}images/run_instance_console_4g.jpg)
Click the Create security group button. The Create security group dialog will close, and the Security group text box will be populated with the name of the security group you just created: 
![image]({{< ref "/" >}}images/run_instance_console_4h.jpg)
You're now ready to launch your new instance. Click the Launch Instance button. The Launch Instance dialog will close, and the Instances screen will display. The instance you just created will display at the top of the list with a status of Pending: 
![image]({{< ref "/" >}}images/run_instance_console_4j.jpg)
When the status of your new instance changes to Running, click the instance in the list to bring up a page showing details of your instance. For example: 
![image]({{< ref "/" >}}images/run_instance_console_4k.jpg)
Note the Public IP address and/or the Public hostname fields. You will need this information to connect to your new instance. For example: 
![image]({{< ref "/" >}}images/run_instance_console_4l.jpg)
Using the public IP address or hostname of your new instance, you can now use SSH to log into the instance using the private key file you saved when you created a key pair. For example: 
    ssh -i my-test-keypair.private root@10.111.57.109 

