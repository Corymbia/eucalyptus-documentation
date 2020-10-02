+++
title = "Install the Data Warehouse"
weight = 10
hidden = true
+++

To install the Data Warehouse on hosts running RHEL 7 or CentOS 7: 


{{% notice note %}}
Do not install the Data Warehouse on a machine running Eucalyptus services. 
{{% /notice %}}
Configure the Eucalyptus package repository on the Data Warehouse host: 
    yum --nogpgcheck install

Install the Data Warehouse packages: 
    yum install eucadw

Install the PostgreSQL server: 
    yum install postgresql91-server

You are now ready to [](configuring_dw.dita) . 