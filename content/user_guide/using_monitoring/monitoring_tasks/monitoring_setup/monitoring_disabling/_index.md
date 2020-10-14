+++
title = "Disable Monitoring"
weight = 20
+++

This section describes steps for disabling monitoring on your cloud resources.To disable monitoring on your resources, following the steps for your resource. 


## Disable monitoring for an instance
To disable monitoring for a running instance, enter the following command: 

    euca-unmonitor-instances [instance_id]


## Disable monitoring for a scaling group
To enable monitoring for an existing Auto Scaling group: Create a launch configuration with `--monitoring-disabled` option. Make a euscale-update-auto-scaling-group request to update your Auto Scaling group with the launch configuration you created in the previous step. Auto Scaling will disable monitoring for new instances that it creates. Choose one of the following actions to deal with all existing instances in the Auto Scaling group: 

| To . . . | Do this . . . | 
|  :---- |  :---- | 
| Preserve existing instances | Make a euca-unmonitor-instances request for all existing instances to disable monitoring. | 
| Terminate existing instances | Make a euscale-terminate-instance-in-auto-scaling-group request for all existing instances. Auto Scaling will use the updated launch configuration to create replacement instances with monitoring disabled. | 

To enable monitoring when you create a new Auto Scaling group: Create a launch configuration with `--monitoring-disabled` option. 
## Disable monitoring for a load balancer
There is no way to disable monitoring for a load balancer. 

