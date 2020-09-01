+++
title = "Back Up Eucalyptus Cloud Data"
weight = 5
chapter = true
+++

..  _backup_euca:



===================
Back Up Cloud Data
===================

This section explains what you need to back up and protect your cloud data.We recommend that you back up the following data: 



* The cloud database: see 

* Object storage. For objects in Walrus, the frequency depends on current load. Use your own discretion to determine the backup plan and strategy. You must have Walrus running. 

* EBS volumes in each cluster (DAS and Overlay) 

* The configuration file for the cloud is stored on the CLC: . 

* Any configuration file for the cloud stored on any other host (UFS, CC, etc.): . 

* The cloud security credentials on all hosts (you already backed up the CLC keys as part of the database backup). Use the tar command: . 

* The CC and NC configuration files, stored on every CC and NC: . 

* Any Euca2ools (.ini) configuration files, which reside on any Euca2ools host machine. Files can be found in: 

* Management Console config files in should be backed up. Typical files: 

* Ensure you have your instances' so you can access the instances later. 

* and LVM snapshots 

* SAN technologies vary, so see the backup documentation for your SAN. 

Users are responsible for volume backups using EBS snapshots on their defined schedules. 

