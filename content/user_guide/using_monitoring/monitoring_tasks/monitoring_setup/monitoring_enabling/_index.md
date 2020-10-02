+++
title = "Enable Monitoring"
weight = 5
+++

This section describes steps for enabling monitoring on your cloud resources.To enable monitoring on your resources, following the steps for your resource. 


## Enable monitoring for an instance
To enable monitoring for a running instance, enter the following command: 
    euca-monitor-instances [instance_id]

To enable monitoring when you launch an instance, enter the following command: 
    euca-run-instances [image_id] -k gsg-keypair --monitor


## Enable monitoring for a scaling group
To enable monitoring for an existing Auto Scaling group: Create a launch configuration with `--monitoring-enabled` option. Make a euscale-update-auto-scaling-group request to update your Auto Scaling group with the launch configuration you created in the previous step. Auto Scaling will enable monitoring for new instances that it creates. Choose one of the following actions to deal with all existing instances in the Auto Scaling group: 
| To . . . | Do this . . . | 
|  :---- |  :---- | 
| Preserve existing instances | Make a euca-monitor-instances request for all existing instances to enable monitoring. | 
| Terminate existing instances | Make a euscale-terminate-instance-in-auto-scaling-group request for all existing instances. Auto Scaling will use the updated launch configuration to create replacement instances with monitoring enabled. | 

To enable monitoring when you create a new Auto Scaling group: Create a launch configuration with `--monitoring-enabled` option. 
## Enable monitoring for a load balancer
Elastic Load Balancing (ELB) sends metrics and dimensions for all load balancers to CloudWatch. By default, you do not need to specifically enable monitoring. 


{{% notice note %}}
ELB only sends CloudWatch metrics when requests are sent through the load balancer. If there are no requests or data for a given metric, ELB does not report to CloudWatch. If there are requests sent through the load balancer, ELB measures and sends metrics for that load balancer in 60-second intervals. 
{{% /notice %}}
