+++
title = "Configure Active Directory"
weight = 10
hidden = true
+++

The Eucalyptus Integration service lets an enterprise with existing Active Directory domains attach Windows instances to the domains and control access to these instances using the existing AD user database. Users can log into the instance either using their domain credentials or the Administrator’s password generated with the `euca-get-password` command. 

Because AD technology is tightly integrated with domain name service (DNS), the default name server contacted by the instance must be able to resolve the AD address as a proper domain controller. You can do this for all networking modes except System, by configuring the following line the CC’s eucalyptus.conf file: 


    VNET_DNS=<domain_controller_IP_address>

If there is no such pre-existing DNS set-up or your networking mode is System, you might need to change the VM’s network interface so that the preferred DNS server points to the domain controller. 

To set up Active Directory: 

Click Windows Programs Eucalyptus Eucalyptus Setup . 
![image]({{< ref "/" >}}images/ewi_win_start.jpg)
The Eucalyptus Windows Integration popup displays. Click the Active Directory tab in the Eucalyptus Windows Integration window and enter the following information: 
![image]({{< ref "/" >}}images/ewi_ad.jpg)


* Enter the domain name of the existing Active Directory domain controller in the field. 
* Enter the administrator username in the field. We recommend using a generic user account that has permission to join a computer to a domain or a specific organizational unit. 
* Enter and confirm the password in the field. Note that the Admin username and password are required to join an instance to an Active Directory. When launched in Eucalyptus, these properties will be deleted as soon as the instance joins (or fails to join) the domain. 
* Optionally, enter an organizational unit in the field. This specifies a container that the instances launched from this image will be attach to. 

{{% notice note %}}
If the values entered in this section are incorrect, the launched instances will fail to join the domain. We recommend that you verify the information by manually joining a computer to a domain using the same information that you entered in this step. You may first log in the launched instance using the administrator password ( ) and manually join the domain for verification. 
{{% /notice %}}
Click Apply . 