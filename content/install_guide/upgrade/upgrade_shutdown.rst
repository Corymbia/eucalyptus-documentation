+++
title = "Shutdown Services"
weight = 5
+++

..  _upgrade_shutdown:

This topic describes how to stop all Eucalyptus services.**Prerequisites** See ` <upgrade_prep.dita#upgrade_prep>`_ for the complete list of upgrade prerequisites. 

The steps you take depend upon where Eucalyptus services are hosted. 

**To shut down Eucalyptus services** 

Log in to the CLC host machine and shut down the CLC service: 

.. code::

  systemctl stop eucalyptus-cloud.service

If you have separate SC host machines, log in to each host and shut down the SC services: 

.. code::

  systemctl stop eucalyptus-cloud.service

If you have a separate Walrus host machine, log in and shut down the Walrus backend services: 

.. code::

  systemctl stop eucalyptus-cloud.service

If you have separate UFS host machines, log in to each host and shut down the UFS services: 

.. code::

  systemctl stop eucalyptus-cloud.service

If there are any other Eucalyptus services (for example Walrus, SC, UFS) co-located on the CC host machine, use this command to shut down the other services on the CC host, and in the correct order: 

.. code::

  systemctl stop eucalyptus-cloud.service

Log in to each CC host machine and shut down the CC service: 

.. code::

  systemctl stop eucalyptus-cluster.service

(Optional) If you are not sure which hosts are *running* eucanetd, check the status on each CLC, CC, and NC: 

.. code::

  systemctl status eucanetd.service

{{% notice note %}}Depending on your network configuration, eucanetd might be running on any of these hosts. Also note that it can be and not . See for more information. {{% /notice %}}Make note of all hosts that have eucanetd *running* ; you'll need this when you `start up the services <upgrade_start.dita#upgrade_start>`_ again. 

Log in to each host machine running eucanetd and shut it down: 

.. code::

  systemctl stop eucanetd.service

Log in to each NC host machine and shut down the NC service: 

.. code::

  systemctl stop eucalyptus-node.service

{{% notice note %}}Running instances on the NC will continue running. For more information see . {{% /notice %}}Log in to each Management Console host machine and shut down the console service: 

.. code::

  systemctl stop eucaconsole.service

You are now ready to ` <upgrade_euca2ools_packages.dita>`_ . 