+++
title = "Configure Remote Desktop"
weight = 10
hidden = true
+++

Domain users or groups require remote desktop permission to log into an instance. By default, only the local administrator has the remote desktop permission. The Eucalyptus Integration Service provides a way to grant remote desktop permission to additional domain users or groups. 

To configure remote desktop permission: 

Open the Eucalyptus Windows Integration popup ( Windows Programs Eucalyptus Eucalyptus Setup ). Click the RemoteDesktop tab 
![image]({{< ref "/" >}}images/ewi_rd.jpg)
The names of authorized domain users and groups display in the Authorized User/Groups field. By default, only the local administrator is listed as authorized. In the text field below the list, enter a user and group account name in the format `[DOMAIN]\[USER or GROUP]` . If you add a new local user or local group, prepend the account name `localhost\` instead of the domain name. Get new image or discard. 
![image]({{< ref "/" >}}images/rdt01.png)
Click Add . Repeat for all user/groups that you want to add. Click Apply . When the instance launches, the members of the groups you added can log in to the instance through remote desktop. 