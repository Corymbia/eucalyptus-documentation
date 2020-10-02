+++
title = "Identity Mapping"
weight = 5
+++

Identities in LDAP/AD are organized differently from the identity structure in Eucalyptus. So a transformation is required to map LDAP/AD identities into Eucalyptus.The following image shows a simple scheme of how the mapping works. In this scheme, the user groups in LDAP tree are partitioned into two sets. Each set is mapped into one separate account. Group 1, 2 and 3 are mapped to Account 1 and Group 4 and 5 are mapped to Account 2. As the result, all users in Group 1, 2 and 3 will be in Account 1, and all users in Group 4 and 5 will be in Account 2. 


![image]({{< ref "/" >}}images/ldap_map.png)
To summarize the mapping method: 



1. Pick user groups from LDAP/AD and combine them into different accounts. There are two ways of doing this: 
1. Once the accounts are defined (by accounting groups or group partitions), all the LDAP/AD user groups will be mapped into Eucalyptus groups within specific accounts; and LDAP/AD users will be mapped into Eucalyptus users. Using the options to filter the groups and users to be imported into Eucalyptus allows granular control. 
1. Groups are group object types in LDAP. The group object type in LDAP/AD needs to have the attribute type determining membership where the value is the Fully Distinguished Name (FDN) of the user(s). Some examples of group object types for LDAP/AD are as follows: 
Note that each group can be mapped into multiple accounts. But understand that Eucalyptus accounts are separate name spaces. So for groups and users that are mapped into different accounts, their information (name, attributes, etc) will be duplicated in different accounts. And duplicated users will have separate credentials in different accounts. For example, Group 1 may map to both Account 1 and Account 2. Say user A belongs to Group 1. Then Account 1 will have user A and Account 2 will also have user A. User A in Account 1 and user A in Account 2 will have different credentials, policies, etc., but the same user information. 


{{% notice note %}}
Currently, there is not a way to map individual users into an account. The mapping unit is LDAP user group. What maps where groups and users end up regarding accounts DEPENDS upon the accounting-groups or groups-partition definitions. 
{{% /notice %}}
