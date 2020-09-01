+++
title = "Configuring the Health Check"
weight = 5
+++

..  _elb_examples_launch_configuration:

To determine which instances are healthy, the load balancer periodically polls the registered instances. You can use the command as described in this topic.Perform the following step to configure how the instances should be polled, how long to wait for a response, and how many consecutive successes or failures are required to mark an instance as healthy or unhealthy. 

{{% notice note %}}After you initially set up your load balancer, Eucalyptus automatically performs a health check to protect against potential side-effects caused by instances being terminated without being deregistered. This health check uses the instance port defined in the load balancer configuration {{% /notice %}}The following shows an example health check configuration command: 

.. code::

  eulb-configure-healthcheck --healthy-threshold 5 --unhealthy-threshold 5 --interval 30 --timeout 120 --target HTTP:80/ MyLoadBalancer

Use ``--healthy-threshold`` and ``--unhealthy-threshold`` to specify the number of consecutive health checks required to mark an instance as Healthy or Unhealthy respectively. Use ``--target`` to specify the connection target on your instances for these health checks. Use ``--interval`` and ``--timeout`` to specify the approximate frequency and maximum duration of these health checks. 

