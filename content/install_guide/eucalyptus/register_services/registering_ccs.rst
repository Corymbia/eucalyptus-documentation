+++
title = "Register the Cluster Controller"
weight = 5
+++

..  _registering_ccs:

This topic describes how to register a Cluster Controller (CC) with the Cloud Controller (CLC).**Prerequisites** 

* The Cloud Controller must be properly installed and started. 

* The Cluster Controller service must be properly installed and started. 

**To register the Cluster Controller service with the Eucalyptus cloud** On the CLC host machine, run the following command: 

.. code::

  euserv-register-service -t cluster -h IP -z ZONE SVCINSTANCE

where: 



* is the IP address of the CC you are registering with this CLC. 

* name should be a descriptive name for the zone controlled by the CC. For example: . 

* must be a unique name for the CC service. We recommend that you use the IP address of the machine, for example: . 

For example: 



.. code::

  euserv-register-service -t cluster -h 10.111.5.182 -z zone-1 cc-10.111.5.182

Copy the security credentials from the CLC to each machine running Cluster Controller services. Run this command on the CLC host machine: 

.. code::

  clcadmin-copy-keys -z ZONE HOST

For example: 



.. code::

  clcadmin-copy-keys -z zone-1 10.111.5.182

Repeat the above steps for each Cluster Controller in each zone. Verify that the Cluster Controller service is registered with the following command: 

.. code::

  euserv-describe-services SVCINSTANCE

The registered Cluster Controller service is now ready for your cloud. 

