+++
title = "Eucalyptus Migration to Edge Networking Mode"
weight = 5
+++

..  _moving_to_edge:

You can configure your existing cloud to use Edge networking mode. This topic provides instructions for configuring and installing additional Eucalyptus components in an existing environment for the purpose of moving to Edge.{{% notice note %}}Migrating to Edge will require downtime of your cloud platform. {{% /notice %}}Terminate all running instances. Find out which instances are running: 

.. code::

  euca-describe-instances

List the instances to terminate: 

.. code::

  euca-terminate-instances instance_id [instance_id ...]

Shut down all Eucalyptus services. For more information, see ` <upgrade_shutdown.dita>`_ . 

.. code::

  systemctl stop eucalyptus-cloud.service

Edit all the config files on NC and CC for Edge networking mode. For more information, see ` <nw_edge.dita>`_ . Install ``eucanetd`` on all NCs. 

.. code::

  yum install eucanetd

Start ``eucanetd`` on all NCs 

.. code::

  systemctl start eucanetd.service

Start all Eucalyptus services: CLC, CC, WS, SC, NCs. For more information, see ` <starting_euca.dita>`_ . Set the Edge JSON property. For more information, see ` <nw_edge.dita#nw_edge_json>`_ . Your Edge networking mode is now properly configured. 