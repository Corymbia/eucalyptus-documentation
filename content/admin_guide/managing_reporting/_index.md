+++
title = "Manage Reporting"
weight = 5
chapter = true
+++


# Manage Reporting
Eucalyptus provides two ways for getting metrics for your cloud: you can get a report directly from the Cloud Controller (CLC), or you can get a report from data exported from the CLC and imported to a data warehouse.
{{% notice note %}}

{{% /notice %}}


When you install Eucalyptus, you automatically get the reporting system in place to generate reports from the CLC. However, the down side to using the CLC for reports is latency. Because of this, Eucalyptus also supports a data warehouse that resides outside the Eucalyptus system to store report data. 

This section describes the concepts and best practices for Eucalyptus reporting, and how to generate reports. 



{{% children %}}
