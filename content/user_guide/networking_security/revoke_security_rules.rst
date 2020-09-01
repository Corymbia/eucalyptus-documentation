+++
title = "Revoke Security Group Rules"
weight = 5
+++

..  _revoke_security_rules:

To revoke security group rules: 

Enter the following command: 

.. code::

  euca-revoke -P <protocol> -p <port_number> -s <CIDR_source_network> <group_name>

The following example revokes the network rules authorized for the security group ``mygroup`` . 



.. code::

  euca-revoke -P tcp -p 22 -s 0.0.0.0/0 mygroup 

