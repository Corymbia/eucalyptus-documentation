+++
title = "Create an HVM image from Windows Installation Media"
weight = 5
chapter = true
+++

..  _images_win:



===================================================
Create an HVM image from Windows Installation Media
===================================================

This section details the tasks necessary to create a Windows image.We recommend that you perform this task on a node controller (NC), or a host running the same Linux distributions and hypervisors as your NCs. If you are creating the Windows image on a machine currently running as a NC, terminate all running instances and stop the NC. To stop the NC, enter: 



.. code::

  systemctl stop eucalyptus-node.service

A template file that closely matches those that Eucalyptus generates at VM instantiation time is located at */usr/share/eucalyptus/doc/libvirt-kvm-windows-example.xml* . We recommend that you review the file to acquaint yourself with its contents, noting required files, bridges, and resources. For more information about configuring the libvirt.xml file, go to the `Domain XML format <http://libvirt.org/formatdomain.html>`_ page in the libvirt documentation. 

