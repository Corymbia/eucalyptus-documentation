+++
title = "Manage ELB Resources"
weight = 5
+++

..  _manage_resources_elb:

To list and delete ELB resources on a Eucalyptus cloud, use the option with any command.The following are some examples. 

To list all detailed configuration information for the load balancers in your cloud, run the following command: 

.. code::

  eulb-describe-lbs verbose

To list the details of policies for all load balancers in your cloud, run the following command: 

.. code::

  eulb-describe-lb-policies verbose

To list meta information for all load balancer policies in your cloud, run the following command: 

.. code::

  eulb-describe-lb-policy-types verbose

To delete any load balancer or any load balancer resource on the cloud, instead of using the ELB name, use the DNS name. For example: 

.. code::

  $ eulb-describe-lbs verbose
  LOAD_BALANCER	MyLoadBalancer	MyLoadBalancer-961915002812.lb.foobar.eucalyptus-systems.com	2013-10-30T03:02:53.39Z
  
  $ eulb-delete-lb MyLoadBalancer-961915002812.lb.foobar.eucalyptus-systems.com 
  $ eulb-describe-lbs verbose 

