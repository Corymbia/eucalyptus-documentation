+++
title = "Installation Overview"
weight = 10
+++

This topic helps you understand, plan for, and install Eucalyptus. If you follow the recommendations and instructions in this guide, you will have a working version of Eucalyptus customized for your specific needs and requirements. This guide walks you through installations for a few different use cases.

{{% notice note %}}
Upgrading to Eucalyptus version 5 from earlier versions is not currently supported.
{{% /notice %}}

You can choose from one of the installation types listed in the following table.

| What Do You Want to Do? | Installation Type | 
|  :---- |  :---- | 
| Quickly deploy on one machine | If you have a CentOS 7.9 minimal install and a few IP addresses to spare, try the FastStart script. Run the following command as root: bash <(curl -Ls https://go.euca.me/5eav) |
| Create a development or production environment | See the [Automated Eucalyptus Installation]({{< relref "automated_install" >}}) section for installation using Ansible |
| Manually create a development or production environment | See the [Manual Eucalyptus Installation]({{< relref "eucalyptus" >}}) section for manual deployment steps |

We recommend that you read the section you choose in the order presented. To customize your installation, you have to understand what Eucalyptus is, what the installation requirements are, what your network configuration and restrictions are, and what Eucalyptus components and features are available based on your needs and requirements.

