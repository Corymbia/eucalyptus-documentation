+++
title = "Using VM Networking and Security"
weight = 70
chapter = true
+++


# Using VM Networking and Security
The Eucalyptus networking mode used, and it's configuration, determine the features available to users; such as elastic IPs, which are public (external) IP addresses that users can reserve and dynamically associate with VM instance; and security groups, which are sets of firewall rules applied to VM instances associated with the group. 

Euca2ools or the AWS CLI provide means for users to interact with these features with commands for allocating and associating IP addresses, as well as creating, deleting, and modifying security groups. 


{{% children sort="weight" %}}
