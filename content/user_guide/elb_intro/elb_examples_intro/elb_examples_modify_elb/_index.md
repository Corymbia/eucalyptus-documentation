+++
title = "Modifying an Elastic Load Balancing Configuration"
weight = 40
+++

Elastic load balancing requires two basic elements to function properly: a load balancer and instances registered with that load balancer. The following examples show how to modify the basic elements of an elastic load balancer configuration.
## De-register instances from the Load Balancer
The load balancer monitors the health of registered instances, and balances incoming traffic across the healthy instances.To deregister an instance from the load balancer: Enter the following command: 

    eulb-deregister-instances-from-lb --instances INSTANCE1,INSTANCE2,... MyLoadBalancer

Enter the following command to verify that the instances are deregistered from the load balancer: `eulb-describe-instance-health MyLoadBalancer` This command will return output similar to the following: 



    INSTANCE	i-6FAD3F7B	InService


## Delete Load Balancer Listeners
To delete a load balancer listener: 

Enter the following command: 

    eulb-delete-lb-listeners --lb-ports PORT1,PORT2,... MyLoadBalancer


## Delete Load Balancer
To delete a load balancer: 

Enter the following command: 

    eulb-delete-lb MyLoadBalancer

You've now deleted the elastic load balancer. 
