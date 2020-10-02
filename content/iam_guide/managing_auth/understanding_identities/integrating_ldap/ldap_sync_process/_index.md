+++
title = "Synchronization Process"
weight = 5
chapter = true
+++


## Synchronization Process
This topic explains what happens to start the synchronization process and what the synchronization process does.The synchronization always starts when the following happens: 



* You manually upload a LDAP/AD Integration Configuration (LIC) file. Every new or updated LIC upload triggers a new synchronization. 
* If the automatic synchronization is enabled, a synchronization is started when the timer goes off. 

{{% notice note %}}
Eucalyptus does not allow concurrent synchronization. If you trigger synchronization more than once within a short time period, Eucalyptus only allows the first one. 
{{% /notice %}}
During a synchronization, everything specified by an LIC in the LDAP/AD tree will be downloaded into Eucalyptus’ internal database. Each synchronization is a merging process of the information already in the database and the information from LDAP/AD. There are three cases for each entity: user, group or account: 



* If an entity from LDAP/AD is not in Eucalyptus, a new one is created in the database. 
* If an entity from LDAP/AD is already in Eucalyptus, the Eucalyptus version is updated. For example, if a user’s info attributes are changed, those changes are downloaded and updated. 
* If an entity in Eucalyptus is missing from LDAP/AD, it will be removed from the database if the clean-deletion option in LIC is set to true. Otherwise, it will be left in the database. 

{{% notice note %}}
If clean-deletion is set to true, the removed entities in Eucalyptus will be lost forever, along with all its permissions and credentials. The resources associated with the entity will be left untouched. It is system administrator’s job to recycle these resources. 
{{% /notice %}}
