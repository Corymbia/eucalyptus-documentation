+++
title = "Start the CLC"
weight = 5
+++

..  _starting_euca_clc:

**Prerequisites** You should have installed and configured Eucalyptus before starting the CLC. 

**To initialize and start the CLC** 

Log in to the Cloud Controller (CLC) host machine. Enter the following command to initialize the CLC: {{% notice note %}}If you are upgrading and you just restored your cloud data, do not initialize the CLC; skip this step. {{% /notice %}}{{% notice note %}}Make sure that the process is running before executing this command. {{% /notice %}}

.. code::

  clcadmin-initialize-cloud

This command might take a minute or more to finish. If it fails, check */var/log/eucalyptus/cloud-output.log* . If you want the CLC service to start at each boot-time, run this command: 

.. code::

  systemctl enable eucalyptus-cloud.service

Enter the following command to start the CLC: 

.. code::

  systemctl start eucalyptus-cloud.service

If you are running in VPCMIDO networking mode: If you want the eucanetd service to start at each boot-time, run this command: 

.. code::

  systemctl enable eucanetd.service

Start the eucanetd service: 

.. code::

  systemctl start eucanetd.service

