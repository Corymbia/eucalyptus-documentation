+++
title = "Hosts"
weight = 10
+++

This topic describes best practices for machines that host a Eucalyptus component.Eucalyptus recommends restricting physical and network access to all hosts comprising the Eucalyptus cloud, and disabling unused applications and ports on all machines used in your cloud. 

After installation, no local access to Eucalyptus component hosts is required for normal cloud operations and all normal cloud operations can be done over remote web service APIs. 

The user-facing services (UFS) and object storage gateway (OSG) are the only two components that generally expect remote connections from end users. Each Eucalyptus component can be put behind a firewall following the list of open ports and connectivity requirements described in the [Configure the Firewall]({{< ref configuring_iptables.md >}}) section. 

For more information on securing Red Hat hosts, see the [Red Hat Enterprise Linux Security Guide](https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/7/html/security_guide/index) . 

