+++
title = "Recover Eucalyptus Cloud Data"
weight = 5
chapter = true
+++


# Recover Cloud Data
This topic explains what to include when you recover your cloud.**Recovering Your Cloud Data** 


{{% notice note %}}
When you recover your cloud data, you need to stop all services, recover the files, then start all services again. 
{{% /notice %}}
We recommend that you recover the following data: 



* The cloud database: see 
* Object storage. For objects in Walrus, the frequency depends on current load. Use your own discretion to determine the restore plan and strategy. 
* EBS volumes in each cluster (DAS and Overlay) 
* The configuration file for the cloud is stored on the CLC: . 
* Any configuration file for the cloud stored on any other host (UFS, CC, etc.): . 
* The cloud security credentials on all hosts (you already restored the CLC keys as part of the database restore). Use the tar command: . 
* The CC and NC configuration files, stored on every CC and NC: . 
* Any Euca2ools (.ini) configuration files, which reside on any Euca2ools host machine. Files in these directories: 
* Management Console config files you backed up from should be restored. Typical files: 
* Ensure you have your instances' so you can access the instances. 
* and LVM snapshots 
* SAN technologies vary, so see the restore documentation for your SAN. 
Users are responsible for volume restore using EBS snapshots. 



{{% children %}}
