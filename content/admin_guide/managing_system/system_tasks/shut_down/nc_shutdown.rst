+++
title = "Shut Down the NCs"
weight = 5
+++

..  _nc_shutdown:

To shut down the NCs perform the steps listed in this topic.To shut down the NCs: 

Log in as root to a machine hosting an NC. Enter the following command: 

.. code::

  systemctl stop eucalyptus-node.service

Repeat for each machine hosting an NC. 