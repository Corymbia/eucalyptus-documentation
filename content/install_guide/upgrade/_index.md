+++
title = "Eucalyptus Upgrade"
weight = 5
chapter = true
+++


## Upgrade
This section details the tasks to upgrade your current version of Eucalyptus .You can upgrade to Eucalyptus 4.4.5 from 4.4.4 (or 4.3.1.1). If your current version is earlier than 4.4.4 , see the prescribed paths below. Follow the directions in that version's Installation Guide in the [documentation archive](../shared/doc_archive.dita#doc_archive) , and then upgrade to 4.4.5 using the directions in this section. 


## Warm upgrade
Eucalyptus supports warm upgrade as of the 3.4.2 release. This means you do not need to shut down EBS-backed or instance-store-backed instances in order to upgrade. Auto Scaling instances will likely shut down and be replaced, based on each group's scaling policy and health check criteria. 


## Prescribed upgrade paths
The following are the prescribed upgrade paths for Eucalyptus versions prior to 4.4 : 

* Upgrade from 3.1.2 to 3.2.2 
* Upgrade from 3.2.2 to 3.3.2 
* Upgrade from 3.3.2 to 3.4.3 
* Upgrade from 3.4.3 to 4.0.2 
* Upgrade from 4.0.2 to 4.1.2 
* Upgrade from 4.1.2 to 4.2.2 
* Upgrade from 4.2.2 to 4.3.1 (see note below) 



{{% notice note %}}
You must have completed the upgrade to 4.3 on RHEL 7 before you can upgrade to 4.4. 
{{% /notice %}}


