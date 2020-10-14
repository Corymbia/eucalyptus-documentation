+++
title = "Creating Elastic Load Balancing Sticky Sessions"
weight = 50
+++

By default, a load balancer routes each request independently to the application instance with the smallest load. However, you can use the sticky session feature (also known as session affinity) which enables the load balancer to bind a user's session to a specific application instance. This ensures that all requests coming from the user during the session will be sent to the same application instance.
## Enable Duration-Based Session Stickiness
To enable duration-based sticky sessions for a load balancer: 

Use the `eulb-create-lb-cookie-stickiness-policy` command to create a load-balancer-generated cookie stickiness policy with a cookie expiration period of 60 seconds. `eulb-create-lb-cookie-stickiness-policy MyLoadBalancer --policy-name MyLoadBalancerPolicy --expiration-period 60` Use the `eulb-set-lb-policies-of-listener` command to enable session stickiness for a load balancer using the MyLoadBalancerPolicy. `eulb-set-lb-policies-of-listener MyLoadBalancer --lb-port 80 --policy-names MyLoadBalancerPolicy` You can use the `eulb-describe-lb-policies` command to list the policies created for the load balancer. `eulb-describe-lb-policies MyLoadBalancer --show-long` 
## Enable Application-Controlled Session Stickiness
To enable application-controlled session stickiness: Use the `eulb-create-app-cookie-stickiness-policy` command to create a load application-generated cookie stickiness policy: `eulb-create-app-cookie-stickiness-policy my-load-balancer -p my-app-cookie-lb-policy -c my-cookie` Use the `eulb-set-lb-policies-of-listener` command to enable session stickiness for a load balancer using the my-load-balancer policy. `eulb-set-lb-policies-of-listener example-lb --lb-port 80 --policy-names my-app-cookie-lb-policy` You can use the `eulb-describe-lb-policies` command to list the policies created for the load balancer. `eulb-describe-lb-policies example-lb --show-long` 
