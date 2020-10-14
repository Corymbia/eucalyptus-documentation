+++
title = "Enabling Cross-Zone Load Balancing"
weight = 110
+++

When an ELB has instances in multiple available zones, enabling cross-zone load balancing will distribute traffics to instances across availability zones. If disabled, the load balancer in a zone will distribute traffics to instances within the zone. For example, if a Zone A has 10 instances, and a Zone B has 1 instance, and the client happens to use the load balancer of Zone B (via round-robin DNS), cross-zone load balancing will ensure that the clients will use all 11 instances, not just the one instance in Zone B.To enable cross-zone load balancing: 

By default, cross-zone load balancing is not enabled for a new load balancer. To enable, modify the load balancer attribute using the eulb-modify-lb-attributes command. For example: `eulb-modify-lb-attributes myloadbalancer CrossZoneLoadBalancing.Enabled=true` Make sure the attribute is enabled. For example: 

    eulb-describe-lb-attributes myloadbalancer
    AccessLog.Enabled false
    ConnectionDraining.Enabled  false
    ConnectionSettings.IdleTimeout 60
    CrossZoneLoadBalancing.Enabled true                

