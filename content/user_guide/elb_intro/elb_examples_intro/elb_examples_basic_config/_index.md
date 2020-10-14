+++
title = "Creating a Basic Elastic Load Balancing Configuration"
weight = 20
+++

Elastic load balancing requires two basic elements to function properly: a load balancer and instances registered with that load balancer. The following examples show how to set up the basic elements of an elastic load balancer configuration.
## Create a Load Balancer
The load balancer manages incoming traffic, and monitors the health of your instances. The load balancer ensures that traffic is only sent to healthy instances.To create a load balancer: 

Enter the following command, specifying availability zones: 

    eulb-create-lb -z one -l "lb-port=80, protocol=HTTP, instance-port=80, 
    instance-protocol=HTTP" MyLoadBalancer

To verify the elastic load balancer has been created, enter the following command: `eulb-describe-lbs MyLoadBalancer` You should see output similar to the following: 



    LOAD_BALANCER	MyLoadBalancer	MyLoadBalancer-587773761872.lb.localhost	2013-01-01T01:23:45.678Z

Optionally, you can create listeners for the load balancer as follows: 

    eulb-create-lb-listeners --listener "lb-port=80, protocol=HTTP,
        instance-port=80, instance-protocol=HTTP"

You've now created an elastic load balancer. 
## Register instances with the Load Balancer
The load balancer monitors the health of registered instances, and balances incoming traffic across the healthy instances.To register an instance with the load balancer: Enter the following command: 

    eulb-register-instances-with-lb --instances i-e0636aca,i-0c9c3967 MyLoadBalancer

Enter the following command to verify that the instances are registered with the load balancer: `eulb-describe-instance-health MyLoadBalancer` This command will return output similar to the following: 



    INSTANCE	i-6FAD3F7B	InService
    INSTANCE	i-70FE4541	InService

Once you've created the load balancer and registered your instances with it, the load balancer will automatically route traffic from its endpoint URL to healthy instances. 
