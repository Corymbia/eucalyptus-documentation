+++
title = "Disable FirewallD on RHEL 7"
weight = 5
+++

This topic describes how to stop and disable FirewallD on RHEL 7.**Prerequisites** 

* You should have successfully installed RHEL 7 before this task. 
If you have existing firewall rules on your host machines, you must disable the firewall in order to install Eucalyptus . You should re-enable it after installation. 
{{% notice note %}}
The firewall on a RHEL 7 system is enabled by default. Before you restart the CLC, you must disable the firewalld service on all host machines. 
{{% /notice %}}


For more information, see [FirewallD on RHEL 7](https://www.certdepot.net/rhel7-get-started-firewalld/) or [FirewallD on CentOS](https://www.digitalocean.com/community/tutorials/how-to-set-up-a-firewall-using-firewalld-on-centos-7) . 

**To stop and disable FirewallD** Check the status of the firewalld service: 
    systemctl status firewalld.service

The status displays as `active (running)` or `inactive (dead)` . If the firewall is active / running, enter this command to stop it: 
    systemctl stop firewalld.service

To completely disable the firewalld service, so it does not reload when you restart the host machine: 
    systemctl disable firewalld.service

Verify the status of the firewalld service: 
    systemctl status firewalld.service

The status should display as `disabled` and `inactive (dead)` . 
    firewalld.service - firewalld - dynamic firewall daemon
      Loaded: loaded (/usr/lib/systemd/system/firewalld.service; disabled; vendor preset: enabled)
      Active: inactive (dead)

Repeat these steps for all host machines. The firewalld service is stopped and disabled. You can now start the CLC and other host machines. 

**Postrequisites** 

* You should re-enable the firewall after installation is complete. 
