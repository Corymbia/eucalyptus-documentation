+++
title = "Euca2ools Standalone Installation"
weight = 20
+++

Euca2ools is the Eucalyptus command line interface for interacting with Eucalyptus. This topic discusses how to perform a standalone installation of Euca2ools. If you're running recent versions of Fedora, Debian, or Ubuntu, you can install Euca2ools using *yum* or *apt*. 

If you're running RHEL/CentOS, you can use the following instructions to install Euca2ools. 

To perform a standalone installation of Euca2ools on RHEL/CentOS: 

Configure the EPEL package repository: 

```bash
yum install epel-release
```

Configure the Euca2ools package repository: 

```bash
yum install http://downloads.eucalyptus.cloud/software/euca2ools/3.4/rhel/7/x86_64/euca2ools-release-3.4-2.2.as.el7.noarch.rpm
```

Install Euca2ools: 

```bash
yum install euca2ools
```

You've now performed a standalone installation of Euca2ools. 
