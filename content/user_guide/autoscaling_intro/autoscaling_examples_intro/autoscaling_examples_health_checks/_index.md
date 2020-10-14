+++
title = "Configuring Health Checks"
weight = 30
+++

By default, Auto Scaling group determines the health state of each instance by periodically checking the results of instance status checks. You can specify using the ELB health check method in addition to using the instance health check method.To use load balancing health checks for an Auto Scaling group: 

Use the following command to specify ELB health checks for an Auto Scaling group: 

    euscale-update-auto-scaling-group MyScalingGroup –-health-check-type ELB –-grace-period 300 

