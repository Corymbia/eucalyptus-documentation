+++
title = "Install Eucalyptus Release Packages"
weight = 10
+++

To install Eucalyptus from release packages, perform the tasks listed in this topic.**Prerequisites** 

* The prerequisite hardware and software should be in place and available to . 
**To install Eucalyptus from release packages** Configure the Eucalyptus package repository on each host machine that will run a Eucalyptus service: 

    yum install 

Enter `y` when prompted to install this package. 

(Optional) If you are a Eucalyptus subscriber, you will receive two RPM package files containing your license for subscription-only services. Install these packages on each host machine that will run a Eucalyptus service. Install the license files to access the enterprise repository. 

    yum install eucalyptus-enterprise-license*.noarch.rpm 

Configure the Euca2ools package repository on each host machine that will run a Eucalyptus service or Euca2ools: 

    yum install 

Enter `y` when prompted to install this package. 

Configure the EPEL package repository on each host machine that will run a Eucalyptus service or Euca2ools: For RHEL/CentOS 7.3 



    yum install 

Enter `y` when prompted to install this package. 

For RHEL/CentOS 7.4 and higher 



    yum install epel-release

Enter `y` when prompted to install this package. 

If you are installing on RHEL 7, you must enable the Optional repository in Red Hat Network for each NC, as follows: Go to [http://rhn.redhat.com](http://rhn.redhat.com) and navigate to the system that will run the NC. Click Alter Channel Subscriptions . Make sure the RHEL Server Optional check-box is selected. Click Change Subscriptions . The following steps should be performed on each NC host machine. Install the Eucalyptus Node Controller software on each NC host: 

    yum install eucalyptus-node

Remove the default libvirt network. This step allows the eucanetd dhcpd server to start. 

    virsh net-destroy default
    virsh net-autostart default --disable

Check that the KVM device node has proper permissions. Run the following command: 



    ls -l /dev/kvm

Verify the output shows that the device node is owned by user root and group kvm. 



    crw-rw-rw- 1 root kvm 10, 232 Nov 30 10:27 /dev/kvm

If your KVM device node does not have proper permissions, you need to reboot your NC host. 

On each CLC host machine, install the Eucalyptus Cloud Controller software. 

    yum install eucalyptus-cloud

Install the backend service image package on the machine hosting the CLC: 

    yum install eucalyptus-service-image

This installs worker images for both the load balancer and imaging services. On the UFS host machine, install the Eucalyptus Cloud Controller software. 

    yum install eucalyptus-cloud

(Optional) On the UFS host machine, also install the Management Console. 

    yum install eucaconsole

The Management Console can run on any host machine, even one that does not have other Eucalyptus services . Install the software for the remaining Eucalyptus services. The following example shows services being installed on the same host machine. We recommend that you use a different host machine for each service, when possible: 

    yum install eucalyptus-cluster eucalyptus-sc eucalyptus-walrus

This installs the cloud controller (CC), storage controller (SC), and Walrus Backend services. (Optional) If you are a subscriber and use a SAN, run the appropriate command for your device on each CLC host machine: For HP 3PAR SAN: 



    yum install eucalyptus-enterprise-storage-san-threepar-libs

For NetApp SAN: 



    yum install eucalyptus-enterprise-storage-san-netapp-libs

For Dell EqualLogic SAN: 



    yum install eucalyptus-enterprise-storage-san-equallogic-libs

(Optional) If you are a subscriber and use a SAN, run the appropriate command for your device on each SC host machine: For HP 3PAR SAN: 



    yum install eucalyptus-enterprise-storage-san-threepar

For NetApp SAN: 



    yum install eucalyptus-enterprise-storage-san-netapp

For Dell EqualLogic SAN: 



    yum install eucalyptus-enterprise-storage-san-equallogic

Your package installation is complete. You are now ready to [Configure Eucalyptus]({{< ref configuring_euca.md >}}) . 