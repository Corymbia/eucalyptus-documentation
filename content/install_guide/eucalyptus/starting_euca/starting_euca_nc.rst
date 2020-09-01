+++
title = "Start the NC"
weight = 5
+++

..  _starting_euca_nc:

**Prerequisites** You should have installed and configured Eucalyptus before starting the NC. 

**To start the NC** 

Log in to the Node Controller (NC) host machine. If you want the NC service to start at each boot-time, run this command: 

.. code::

  systemctl enable eucalyptus-node.service

Enter the following command to start the NC: 

.. code::

  systemctl start eucalyptus-node.service

If you are running in EDGE networking mode: If you want the eucanetd service to start at each boot-time, run this command: 

.. code::

  systemctl enable eucanetd.service

Start the eucanetd service: 

.. code::

  systemctl start eucanetd.service

Repeat for each NC host machine. 