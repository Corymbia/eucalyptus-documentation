+++
title = "Register the Walrus Backend"
weight = 5
+++

..  _registering_walruses:

This topic describes how to register the Walrus Backend service with the Cloud Controller (CLC).**Prerequisites** 

* You must be using the Walrus Backend service as your object storage provider. 

* The Cloud Controller must be properly installed and started. 

**To register the Walrus Backend service with the Eucalyptus cloud** {{% notice note %}}This task is not necessary if you are using Riak CS instead of Walrus. {{% /notice %}}On the CLC host machine, run the following command: 

.. code::

  euserv-register-service -t walrusbackend -h IP SVCINSTANCE

where: 



* is the IP of the Walrus Backend you are registering with this CLC. 

* must be a unique name for the Walrus Backend service. We recommend that you use a short-hand name of the hostname or IP address of the machine, for example: or . 

For example: 



.. code::

  euserv-register-service -t walrusbackend -h 10.111.5.182 walrus-10.111.5.182

Copy the security credentials from the CLC to each machine running a Walrus Backend service. Run this command on the CLC host machine: 

.. code::

  clcadmin-copy-keys HOST [HOST ...]

For example: 



.. code::

  clcadmin-copy-keys 10.111.5.182

Verify that the Walrus Backend service is registered with the following command: 

.. code::

  euserv-describe-services SVCINSTANCE

The registered Walrus Backend service is now ready for your cloud. 

