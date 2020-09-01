+++
title = "Eucalyptus ELB Listener Configurations"
+++

..  _elb_listener_configs:

This section provides a reference to various possible ways to configure your listener, depending on how secure you want your load balancer. Currently, Eucalyptus supports the following HTTP/HTTPS Load Balancer use cases: 

* Basic HTTP load balancer 

* Secure website or application using ELB to offload SSL decryption. 

* Secure website or application using end-to-end encryption 





.. list-table::
  :header-rows: 1

  *
    - Use Case
    - Front-end Protocol
    - Front-end Options
    - Back-end Protocol
    - Back-end Options
    - Notes
  *
    - Basic HTTP load balancer
    - HTTP
    - NA
    - HTTP
    - NA
    - Supports X-forward for header. Go to AWS X-forwarding for more information.
  *
    - Secure website or application using Elastic Load Balancing to offload SSL decryption
    - HTTPS
    - SSL Negotiation. See .`../user-guide/elb_examples_ssl_negotiation <{{< relref "elb_examples_ssl_negotiation" >}}>`__
    - HTTP
    - NA
    - Supports X-forward for header. Go to AWS X-forwarding for more information. Requires an SSL certificate installed on the load balancer.
  *
    - Secure website or application using end-to-end encryption
    - HTTPS
    - SSL Negotiation. See .`../user-guide/elb_examples_ssl_negotiation <{{< relref "elb_examples_ssl_negotiation" >}}>`__
    - HTTPS
    - Back-end authentication
    - Supports X-forward for header. Go to AWS X-forwarding for more information. Requires an SSL certificate installed on the load balancer and registered instances.


