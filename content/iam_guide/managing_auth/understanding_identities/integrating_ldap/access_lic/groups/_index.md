+++
title = "groups"
weight = 5
+++

The element specifies how to map LDAP/AD groups to Eucalyptus groups. It contains the elements listed in the following table. The meanings are similar to those in accounting-groups element.
| Element | Description | 
|  :---- |  :---- | 
| base-dn | The base DN for searching groups. | 
| id-attribute | The ID attribute name of the LDAP group. | 
| member-attribute | The name of the attribute for group members. Usually, it is member in modern LDAP implementation, which lists full user DN. | 
| selection | The specific LDAP/AD groups you want to map to. This contains the following elements: filter: The LDAP/AD searching filter used for the LDAP/AD search to get the relevant LDAP/AD entities, e.g. the users to be synchronized. (Example: objectClass=groupOfNames). This element works the same as the filter option that is found in ldapsearch, therefore when doing more advanced searching using compound filters, use boolean operators - AND (&), OR (|), and/or NOT (!). (Example: (&(ou=Sales)(objectClass=groupOfNames))select: The LDAP/AD searching filter used for the LDAP/AD search to get the relevant LDAP/AD entities, e.g. the users to be synchronized. (Example: objectClass=groupOfNames)not-select: Explicitly gives the full DN of entities NOT to be synchronized, in case this can not be specified by the search filter. (Example: cn=groupToIgnore,ou=Groups,dc=foo,dc=com) | 

