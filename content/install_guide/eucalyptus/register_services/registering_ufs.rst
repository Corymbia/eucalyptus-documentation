+++
title = "Register User-Facing Services"
weight = 5
+++

..  _registering_services:

This topic describes how to register the User-Facing Services (UFS) with the Cloud Controller (CLC).**Prerequisites** 

* The Cloud Controller must be properly installed and started. 

* The User-Facing Services must be properly installed and started. 

**To register the User-Facing Services with the Eucalyptus cloud** On the CLC host machine, obtain your temporary access keys for the Eucalyptus set up by running the following command: 

.. code::

  eval `clcadmin-assume-system-credentials`

{{% notice note %}}You will create longer-lived and fully functional access keys later. {{% /notice %}}Also on the CLC host machine, run the following command: 

.. code::

  euserv-register-service -t user-api -h IP SVCINSTANCE

where: 



* is the IP address of the UFS you are registering. 

* must be a unique name for the User-Facing service. 

For example: 



.. code::

  euserv-register-service -t user-api -h 10.111.5.183 user-api-1

Repeat for each UFS host, replacing the UFS IP address and UFS name. Copy the security credentials from the CLC to each machine running User-Facing Services. Run this command on the CLC host machine: 

.. code::

  clcadmin-copy-keys HOST [HOST ...]

For example: 



.. code::

  clcadmin-copy-keys 10.111.5.183

Verify that the User-Facing service is registered with the following command for each instance of the UFS: 

.. code::

  euserv-describe-services SVCINSTANCE

The registered UFS instances are now ready for your cloud. 

