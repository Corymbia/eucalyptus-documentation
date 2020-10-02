+++
title = "accounting-groups"
weight = 5
+++

This section uses a special group in LDAP/AD to designate accounts in the Eucalyptus “accounting group.” The accounting group takes normal LDAP/AD groups as members, i.e., they are groups of groups.The accounting group’s name becomes the account name in Eucalyptus. The member groups become Eucalyptus groups in that account. And the users of all those groups become Eucalyptus users within that account and corresponding Eucalyptus groups. 


{{% notice note %}}
If you use , remove the section. These two sections are mutually exclusive. 
{{% /notice %}}

| Element | Description | 
|  :---- |  :---- | 
| base-dn | The base DN of accounting groups in the LDAP/AD tree. | 
| id-attribute | The ID attribute name of the accounting group entry in LDAP/AD tree. | 
| member-attribute | The LDAP/AD attribute name for members of the accounting group. | 
| selection | The accounting groups you want to map to. This contains the following elements: filter: The LDAP/AD searching filter used for the LDAP/AD search to get the relevant LDAP/AD entities, e.g. the users to be synchronized. (Example: objectClass=groupOfNames). This element works the same as the filter option that is found in ldapsearch, therefore when doing more advanced searching using compound filters, use boolean operators - AND (&), OR (|), and/or NOT (!). (Example: (&(ou=Sales)(objectClass=groupOfNames))select: Explicitly gives the full DN of entities to be synchronized, in case they can not be specified by the search filter. (Example: cn=groupToSelect,ou=Groups,dc=foo,dc=com)not-select: Explicitly gives the full DN of entities NOT to be synchronized, in case this can not be specified by the search filter. (Example: cn=groupToIgnore,ou=Groups,dc=foo,dc=com) | 

