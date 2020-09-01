+++
title = "Start the SC"
weight = 5
+++

..  _starting_euca_sc:

**Prerequisites** You should have installed and configured Eucalyptus before starting the SC. 

{{% notice note %}}If you are re-installing the SC, restart the tgt (iSCSI open source target) daemon. {{% /notice %}}{{% notice note %}}If you installed SC on the same host as the CLC, you can skip this. {{% /notice %}}**To start the SC** 

Log in to the Storage Controller (SC) host machine. If you want the SC service to start at each boot-time, run this command: 

.. code::

  systemctl enable eucalyptus-cloud.service

If you want the tgtd service to start at each boot-time, run this command: 

.. code::

  systemctl enable tgtd.service

{{% notice note %}}depends on tgtd to create and manage block storage volumes when the storage provider is either DAS or Overlay. {{% /notice %}}Enter the following commands to start the SC: 

.. code::

  systemctl start tgtd.service



.. code::

  systemctl start eucalyptus-cloud.service

If you have a multi-zone setup, repeat this step on the SC in each zone. 