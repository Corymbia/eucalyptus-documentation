+++
title = "LDAP/AD Integration"
weight = 5
chapter = true
+++


## LDAP/AD Integration
You can use the Eucalyptus LDAP/Active Directory (AD) integration to synchronize existing LDAP/AD user and group information with Eucalyptus.When you enable LDAP/AD synchronization, Eucalyptus imports specified user and group information from LDAP or AD and maps them into a predefined two-tier account/group/user structure 

Note that Eucalyptus only imports the identities and some related information. Any Eucalyptus-specific attributes are still managed from Eucalyptus. These include: 



* User credentials: secret access keys and X.509 certificates. 
* Policies: IAM policies and quotas. Policies are associated with identities within Eucalyptus, and stored in internal database. 
Also note that special identities, including system administrators and account administrators, are created in Eucalyptus and not imported from LDAP/AD. Only normal user identities are imported. 


{{% notice note %}}
If you integrate LDAP/AD, you do not need to create IAM user login profiles for your users. The "admin" user has the ability to change the passwords of other users in the account through . This only applies if LDAP/AD integration is not enabled. If LDAP/AD integration is enabled, the only passwords that can be changed are users not associated with LDAP/AD. These users are as follows: 


{{% /notice %}}
