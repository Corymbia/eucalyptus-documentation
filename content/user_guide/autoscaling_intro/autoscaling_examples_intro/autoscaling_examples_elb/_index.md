+++
title = "Configuring Auto Scaling with Elastic Load Balancing"
weight = 50
+++

This example shows how to set up Auto Scaling with Elastic Load Balancing.To set up a load-balanced auto scaling configuration: 

If you don't already have a launch configuration, create one: `euscale-create-launch-config MyLaunchConfig --image-id emi-50783D25 --instance-type m1.medium --group mysecuritygroup` Create a new auto scaling group associated with a load balancer: `euscale-create-auto-scaling-group MyScalingGroup --launch-configuration MyLaunchConfig --load-balancers MyLoadBalancer --availability-zones AcmeAvailabilityZone --min-size 2 --max-size 4` Authorize the security group used by the load balancer for back-end port communication. For example: 

    $ eulb-describe-lbs --show-long
    LOAD_BALANCER	MyLoadBalancer	MyLoadBalancer-408396244283.elb.acme.eucalyptus-systems.com			
    {interval=200,target=HTTP:80/,timeout=3,healthy-threshold=2,unhealthy-threshold=4}		AcmeAvailabilityZone		
    {protocol=HTTP,lb-port=80,instance-protocol=HTTP,instance-port=80}					
    {owner-alias=944786667073,group-name=euca-internal-408396244283-MyLoadBalancer}		
    2014-05-28T18:13:17.902Z

`euca-authorize mysecuritygroup -u 944786667073 -o euca-internal-408396244283-MyLoadBalancer -p -1` Verify that your Auto Scaling group has been created with a load balancer: 

    $ euscale-describe-auto-scaling-groups
    AUTO-SCALING-GROUP	MyScalingGroup	MyLaunchConfig	AcmeAvailabilityZone	MyLoadBalancer	2	4	2	Default
    INSTANCE	i-DFCD0CBC	AcmeAvailabilityZone	InService	Healthy	MyLaunchConfig
    INSTANCE	i-B3431043	AcmeAvailabilityZone	InService	Healthy	MyLaunchConfig

