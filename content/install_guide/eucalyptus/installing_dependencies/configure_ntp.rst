+++
title = "Configure NTP"
weight = 5
+++

..  _configure_ntp:



To use NTP: 

Install NTP on the machines that will host Eucalyptus components. 

.. code::

  yum install ntp

Open the */etc/ntp.conf* file and add NTP servers, if necessary, as in the following example. 

.. code::

  server 0.pool.ntp.org
  server 1.pool.ntp.org
  server 2.pool.ntp.org

Save and close the file. Synchronize your server. 

.. code::

  ntpdate -u YOUR_NTP_SERVER

Configure NTP to run at reboot. 

.. code::

  systemctl enable ntpd.service

Start NTP. 

.. code::

  systemctl start ntpd.service

Synchronize your system clock, so that when your system is rebooted, it does not get out of sync. 

.. code::

  hwclock --systohc

Repeat on each host machine that will run a Eucalyptus service. 