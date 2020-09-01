+++
title = "Manage Compute Resources"
weight = 5
+++

..  _manage_resources_ec2:

To manage compute resources on a Eucalyptus cloud, use the option in any command.The following are some examples you can use to view various compute resources. For more information about compute commands, see ` <../euca2ools-guide/euca.dita>`_ . 

To see all instances running on your cloud, enter the following command: 

.. code::

  euca-describe-instances verbose

To see all volumes in your cloud, enter the following command: 

.. code::

  euca-describe-volumes verbose

To see all keypairs in your cloud, enter the following command: 

.. code::

  euca-describe-keypairs verbose

