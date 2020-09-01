+++
title = "Change Multicast Address"
weight = 5
+++

..  _modify_multicast:

This topic describes how to change your multicast address for group membership.By default, Eucalyptus uses the multicast address 239.193.7.3 for group membership. Most data centers limit multicast address communication for security measures. We recommend that you use addresses in the administratively-scoped multicast address range. {{% notice note %}}As of Eucalyptus 4.3, the default multicast address changed from 228.7.7.3 to 239.193.7.3. {{% /notice %}}

**To change the multicast address for group membership** Stop all services, starting from the CC, SC, Walrus, then CLC. For example: 

.. code::

  systemctl stop eucalyptus-cluster.service
  systemctl stop eucalyptus-cloud.service

Change the *eucalyptus.conf* on the CC, modifying the ``CLOUD_OPTS`` parameter to the new IP address: 

.. code::

  CLOUD_OPTS="--mcast-addr=228.7.7.3"

{{% notice note %}}The above shows how to set the multicast address to a value compatible with releases prior to Eucalyptus 4.3. {{% /notice %}}Restart all services, starting from the CLC, Walrus, SC, CC. For example: 

.. code::

  systemctl start eucalyptus-cloud.service
  systemctl start eucalyptus-cluster.service

Verify that the configured multicast address is being used via netstat: 

.. code::

  netstat -nulp

**Postrequisites** 

* Check the firewall after changing the multicast address. See for more information. 

