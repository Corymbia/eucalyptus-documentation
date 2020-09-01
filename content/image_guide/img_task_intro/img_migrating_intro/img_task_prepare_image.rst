+++
title = "Prepare a Linux System for Eucalyptus"
weight = 5
+++

..  _hg_task_prepare_image:

This section explains how to prepare a running Linux system (cloud instance, virtual machine, or a system running on bare metal) before importing it for use in Eucalyptus.**Install cloud software and drivers:** Make sure Virtio drivers are installed if the image is going to be run in a KVM cluster which has virtio enabled, and verify use if possible (ie. set disks and network interface in hypervisor, try hot plug in for disks, etc). For most recent Linux distributions nothing is needed to be done. Make sure appropriate init scripts are in place; for example: cloud-init packages (if appropriate), and rc.local or similar scripts to prepare new instances at boot time utilizing user/meta-data. Install cloud-init: {{% notice note %}}For more information on cloud-init, go to {{% /notice %}}For Red Hat, and CentOS EL7: 



.. code::

  rpm -Uvh http://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm
  yum install cloud-init

Install and configure ssh: For Red Hat and CentOS: 



.. code::

  yum install openssh-server
  systemctl enable sshd.service

Install Euca2ools: For Red Hat and CentOS: 



.. code::

  yum install euca2ools

Optionally, update existing packages. For Red Hat and CentOS: 



.. code::

  yum update

**Prepare the network:** Disable the firewall. It is recommended that the firewall is disabled and network rules are instead enforced in the security-group the instances run in. If the guest's firewall is not disabled, review the existing rules and make sure they are appropriate for the guest's future use within a cloud environment. Clear or disable iptable rules: Save the rules in case you want to restore them later: 



.. code::

  sudo iptables-save > /root/firewall.rules

Clear the rules: 



.. code::

  iptables -F
  iptables -X
  iptables -t nat -F
  iptables -t nat -X
  iptables -t mangle -F
  iptables -t mangle -X
  iptables -P INPUT ACCEPT
  iptables -P OUTPUT ACCEPT
  iptables -P FORWARD ACCEPT

For Red Hat and CentOS 6, you can disable iptables via service scripts. For example: 



.. code::

  service iptables stop
  (then use...) 
  chkconfig iptables off  (to disable at boot time as well) 

For Red Hat and CentOS 7, see the Red Hat Migration and Planning Guide `Security and Access Control section <https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/Migration_Planning_Guide/sect-Red_Hat_Enterprise_Linux-Migration_Planning_Guide-Security_and_Access_Control.html>`_ . 

Make sure there is only a single primary network interface. Check the configuration for: 



* Enabled on boot ( ) 

* IP provisioning is done via DHCP ( ) 

* MAC address is commented out (for example: ). 

For Red Hat and CentOS images, the configuration for the default network interface can usually be found in the following file: 



.. code::

  /etc/sysconfig/network-scripts/ifcfg-eth0

The following is an example of an ``ifcfg-eth0`` configuration file: 



.. code::

  DEVICE=eth0
  ONBOOT=yes
  #THE HWADDR LINE MUST BE COMMENTED OUT OR REMOVED
  #HWADDR=AA:BB:CC:DD:EE:FF
  TYPE=Ethernet
  BOOTPROTO=dhcp
  PERSISTENT_DHCLIENT=yes

Remove persistent udev rules: 

.. code::

  echo "" > /etc/udev/rules.d/70-persistent-net.rules 
  echo "" > /lib/udev/rules.d/75-persistent-net-generator.rules 

On CentOS and Red Hat, disable zeroconf by adding an entry to the ``/etc/sysconfig/network`` file: 

.. code::

  NETWORKING=yes
  NOZEROCONF=yes

**Clean the image:** We recommend that you remove all non-root, non-administrator users before bundling the image. Remove root/Administrator password. We recommend that you remove root's password for Linux systems (for windows, use sysprep (see Administrators guide for Windows Integration tool). {{% notice note %}}Once these passwords are removed, access to this system will be limited or blocked until this image is recreated as a cloud instance. SSH host and authorization keys for Linux (or dynamically created passwords for Windows sysprep) will be used going forward. {{% /notice %}}For larger Windows images, we recommend that you use the tool of your choice to zero out unused disk space. Remove any unwanted programs. Configure a serial port by adding an option to the end of the ``/boot/grub/menu.lst`` file: ``console=ttyS0`` You've now prepared your instance for image creation. 