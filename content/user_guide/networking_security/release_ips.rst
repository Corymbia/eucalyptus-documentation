+++
title = "Release an IP Address"
weight = 5
+++

..  _release_ips:

Use euca-disassociate-address and euca-release-address to disassociate an IP address from an instance and to release the IP address to the global pool, respectively. 

To release an IP address: 

Enter the following command to disassociate an IP address from an instance: 

.. code::

  euca-disassociate-address <IP_address>

Enter the following command to release an IP address: 

.. code::

  euca-disassociate-address <IP_address>

The following example releases the IP address, ``192.168.17.103`` 



.. code::

  euca-release-address 192.168.17.103

