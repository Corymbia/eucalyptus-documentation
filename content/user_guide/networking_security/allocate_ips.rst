+++
title = "Associate an IP Address with an Instance"
weight = 5
+++

..  _allocate_ips:

To associate an IP address with an instance: 

Allocate an IP address: 

.. code::

  euca-allocate-address ADDRESS <IP_address>

Associate the allocated IP address with an instance ID: 

.. code::

  euca-associate-address -i <instance_ID> <IP_address> 



.. code::

  euca-associate-address -i i-56785678 192.168.17.103

