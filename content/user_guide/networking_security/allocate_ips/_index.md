+++
title = "Associate an IP Address with an Instance"
weight = 10
+++

To associate an IP address with an instance: 

Allocate an IP address: 

    euca-allocate-address ADDRESS <IP_address>

Associate the allocated IP address with an instance ID: 

    euca-associate-address -i <instance_ID> <IP_address> 



    euca-associate-address -i i-56785678 192.168.17.103

