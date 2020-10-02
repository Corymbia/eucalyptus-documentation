+++
title = "sync"
weight = 10
+++

The element contains elements for controlling synchronization.

| Element | Description | 
|  :---- |  :---- | 
| enable | Set to "true" to enable LDAP synchronization. When this is “false”, all other fields can be ignored. Default value: false | 
| auto | Set to true to turn on automatic synchronization. Set to false to turn off synchronization. | 
| interval | The length in milliseconds of the automatic synchronization interval. | 
| clean-deletion | Parameter denoting whether to remove identity entities from Eucalyptus when they are deleted from LDAP. Set to true if you want Eucalyptus to remove any identities once their counterparts in LDAP are deleted. Set to false if you want these identities kept without being purged. | 

