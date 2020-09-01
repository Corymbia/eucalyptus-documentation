+++
title = "Shut Down the CCs"
weight = 5
+++

..  _cc_shutdown:

To shut down the CCs: 

Log in as root to a machine hosting a CC. Enter the following command: 

.. code::

  systemctl stop eucalyptus-cluster.service

Repeat for each machine hosting a CC. 