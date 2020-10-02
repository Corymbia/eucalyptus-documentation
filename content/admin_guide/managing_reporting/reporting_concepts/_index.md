+++
title = "Reporting Overview"
weight = 5
chapter = true
+++


# Reporting Overview
Eucalyptus lets you generate reports to monitor cloud resource use. Each type of report is for a specified time range.Eucalyptus supports the following report types: 



* The instance report provides information about the amount, duration, and utilization of all running instances. Use this report to understand how many instances each user is running, whether your instance types are large enough, etc. 
* The S3 report provides information about the number of buckets and objects stored in Walrus. Empty buckets are not reported. Use this report to understand the storage needs of each user and your cloud's storage needs. 
* The volume report provides information about the amount, duration, and size of all volumes in use. Use this report to understand how many volumes are running, and what the storage size of each volume is. 
* The snapshot report provides information about the amount of your cloud's snapshots. Use this report to understand how many snapshots there are and from which volumes, and what the size of each snapshot is. 
* The elastic IP report provides information about the lifecycle of elastic IPs in your cloud, including which user is using which IPs, which IPs are currently in use, and how often and for how long does IP get allocated. Use this report to understand how many IPs each user is assigned and to which instance the IP is assigned to, and the running time of each IP. 
* The capacity report provides overall information about your cloud's resources, including instance types and storage. Use this report to determine if your resources are being used adequately, and whether you need to scale up or down. 
You can generate reports in either CSV or HTML formats for use with external tools. 

If you want to use the data warehouse for your reports, see [](setting_up_dw.dita) . 


## Understanding the Report Format
All Eucalyptus reports contain a usage section. The instance report also contains a running time section. 

The usage section shows cumulative ( cumul. ) metrics for each zone, account, and user. Then the report lists metrics for each resource. The column for each resource type (for example, Instance Id or Volume Id displays cumul. for all cumulative metrics. When individual resources are reported, the individual resource's name or identifier displays in that column. 



{{% children %}}
