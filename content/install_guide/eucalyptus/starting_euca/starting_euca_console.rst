+++
title = "Start the Management Console"
weight = 5
+++

..  _starting_euca_clc:

**Prerequisites** The link to the shared topics below need to be drupal-ified! Before you start the Management Console, ensure that you have reviewed the ` <../shared/console_configure_intro.dita#console_configure_intro/console_configure_intro_requirements>`_ in the `Management Console Guide <../console-guide/index.dita>`_ . {{% notice note %}}If you plan on running multiple Management Console host machines, we recommend turning off the default memcached in your console.ini file. See for details. {{% /notice %}}

Log in to the Management Console host machine. If you want the console service to start at each boot-time, run this command: 

.. code::

  systemctl enable eucaconsole.service

Enter the following command to start the console: 

.. code::

  systemctl start eucaconsole.service

Repeat for each Management Console host machine. 