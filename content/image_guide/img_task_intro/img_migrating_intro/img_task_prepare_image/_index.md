+++
title = "Prepare a Linux System for Eucalyptus"
weight = 30
+++

This section explains how to prepare a running Linux system (cloud instance, virtual machine, or a system running on bare metal) before importing it for use in Eucalyptus.**Install cloud software and drivers:** Make sure Virtio drivers are installed if the image is going to be run in a KVM cluster which has virtio enabled, and verify use if possible (ie. set disks and network interface in hypervisor, try hot plug in for disks, etc). For most recent Linux distributions nothing is needed to be done. Make sure appropriate init scripts are in place; for example: cloud-init packages (if appropriate), and rc.local or similar scripts to prepare new instances at boot time utilizing user/meta-data. 

Install cloud-init: 

{{% notice note %}}
For more information on cloud-init, go to https://help.ubuntu.com/community/CloudInit
{{% /notice %}}

For Red Hat Enterprise Linux, and CentOS 7: 

    yum install cloud-init

Install and configure ssh: For Red Hat and CentOS: 

    yum install openssh-server
    systemctl enable sshd.service

Install Euca2ools: For Red Hat and CentOS: 

    yum install euca2ools

Optionally, update existing packages. For RHEL and CentOS:

    yum update

**Prepare the network:** Disable the firewall. It is recommended that the firewall is disabled and network rules are instead enforced in the security-group the instances run in. If the guest's firewall is not disabled, review the existing rules and make sure they are appropriate for the guest's future use within a cloud environment. Clear or disable iptable rules: Save the rules in case you want to restore them later: 

    sudo iptables-save > /root/firewall.rules

Clear the rules: 

    iptables -F
    iptables -X
    iptables -t nat -F
    iptables -t nat -X
    iptables -t mangle -F
    iptables -t mangle -X
    iptables -P INPUT ACCEPT
    iptables -P OUTPUT ACCEPT
    iptables -P FORWARD ACCEPT

For RHEL and CentOS 7, see the Red Hat Migration and Planning Guide [Security and Access Control section](https://access.redhat.com/documentation/en-US/Red_Hat_Enterprise_Linux/7/html/Migration_Planning_Guide/sect-Red_Hat_Enterprise_Linux-Migration_Planning_Guide-Security_and_Access_Control.html) . 

Make sure there is only a single primary network interface. Check the configuration for: 

* Enabled on boot (ONBOOT="yes") 
* IP provisioning is done via DHCP (BOOTPROTO="dhcp")
* MAC address is commented out (for example: #HWADDR="AA:BB:CC:DD:EE:FF")

For RHEL and CentOS images, the configuration for the default network interface can usually be found in the following file:

    /etc/sysconfig/network-scripts/ifcfg-eth0

The following is an example of an `ifcfg-eth0` configuration file: 

    DEVICE=eth0
    ONBOOT=yes
    #THE HWADDR LINE MUST BE COMMENTED OUT OR REMOVED
    #HWADDR=AA:BB:CC:DD:EE:FF
    TYPE=Ethernet
    BOOTPROTO=dhcp
    PERSISTENT_DHCLIENT=yes

Remove persistent udev rules: 

    echo "" > /etc/udev/rules.d/70-persistent-net.rules 
    echo "" > /lib/udev/rules.d/75-persistent-net-generator.rules 

On CentOS and RHEL, disable zeroconf by adding an entry to the `/etc/sysconfig/network` file: 

    NETWORKING=yes
    NOZEROCONF=yes

**Clean the image:** We recommend that you remove all non-root, non-administrator users before bundling the image. Remove root/Administrator password. We recommend that you remove root's password for Linux systems. 
{{% notice note %}}
Once these passwords are removed, access to this system will be limited or blocked until this image is recreated as a cloud instance. SSH host and authorization keys for Linux  will be used going forward. 
{{% /notice %}}
Remove any unwanted programs. Configure a serial port by adding an option to the end of the `/boot/grub/menu.lst` file: `console=ttyS0` You've now prepared your instance for image creation. 
