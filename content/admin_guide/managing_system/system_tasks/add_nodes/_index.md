+++
title = "Add a Node Controller"
weight = 40
+++

If you want to increase your system’s capacity, you’ll want to add more Node Controllers (NCs).To add an NC, perform the following tasks: 

Log in to the CLC and enter the following command: 

    clusteradmin-register-nodes node0_IP_address ... [nodeN_IP_address]

When prompted, enter the password to log into each node. Eucalyptus requires this password to propagate the cryptographic keys. 
