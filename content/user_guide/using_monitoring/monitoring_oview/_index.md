+++
title = "CloudWatch Overview"
weight = 10
chapter = true
+++


# CloudWatch Overview
This section describes the concepts and details you need to understand the CloudWatch service. This section also includes procedures to complete the most common tasks for CloudWatch.CloudWatch is a Eucalyptus service that collects, aggregates, and dispenses data from your cloud's resources. This data allows you to make operational and business decisions based on actual performance metrics. You can use CloudWatch to collect metrics about your cloud resources, such as the performance of your instances. You can also publish your own metrics directly to CloudWatch. 

CloudWatch monitors the following cloud resources: 



* instances 
* Elastic Block Store (EBS) volumes 
* Auto Scaling instances 
* Eucalyptus Load Balancers (ELB) 

## Alarms
CloudWatch alarms help you make decisions more easily by automatically making changes to the resources you are monitoring, based on rules that you define. For example, you can create alarms that initiate Auto Scaling actions on your behalf. For more information about alarm tasks, see [Configuring Alarms]({{< ref monitoring_alarm.md >}}) . 


## Common Use Cases
A common use for CloudWatch is to keep your applications and services healthy and running efficiently. For example, CloudWatch can determine that your application runs best when network traffic remains below a certain threshold level on your instances. You can then create an automated procedure to ensure that you always have the right number of instances to match the amount of traffic you have. 

Another use for CloudWatch is to diagnose problems by looking at system performance before and after a problem occurs. CloudWatch helps you identify the cause and verify your fix by tracking performance in real time. 



{{% children sort="weight" %}}
