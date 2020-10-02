+++
title = "users"
weight = 10
hidden = true
+++

Explicitly gives the full DN of entities NOT to be synchronized, in case this can not be specified by the search filter.

| Element | Description | 
|  :---- |  :---- | 
| base-dn | The base DN for searching users. | 
| id-attribute | The attribute ID of the LDAP user. | 
| selection | The specific LDAP/AD users you want to map to. This contains the following elements: filter: The LDAP/AD searching filter used for the LDAP/AD search to get the relevant LDAP/AD entities, e.g. the users to be synchronized. (Example: objectClass=organizationalPerson). This element works the same as the filter option that is found in ldapsearch, therefore when doing more advanced searching using compound filters, use boolean operators - AND (&), OR (|), and/or NOT (!). (Example: (&(ou=Sales)(objectClass=organizationalPerson)))select: Explicitly gives the full DN of entities to be synchronized, in case they can not be specified by the search filter. (Example: cn=userToSelect,ou=People,dc=foo,dc=com)not-select: Explicitly gives the full DN of entities NOT to be synchronized, in case this can not be specified by the search filter. (Example: cn=userToIgnore,ou=People,dc=foo,dc=com) | 

