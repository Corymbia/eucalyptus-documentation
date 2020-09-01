+++
title = "groups-partition"
weight = 5
+++

..  _groups_partition:

Like accounting-groups, groups-partition specifies how to map LDAP/AD groups to Eucalyptus accounts. However, in this section you to manually specify which LDAP/AD groups you want to map to Eucalyptus accounts.{{% notice note %}}If you use , remove the section. These two sections are mutually exclusive. {{% /notice %}}The Eucalyptus accounts are created by partitioning LDAP/AD groups. Each partition composes an Eucalyptus account. So all the groups within the partition become Eucalyptus groups within that account. All the users of those groups will become Eucalyptus users within that account and the corresponding Eucalyptus groups. 

This section requires that you specify one partition at a time, using a list of JSON key-value pairs. For each entry, the key is the account name to be mapped and the value is a list of names of LDAP/AD groups to be mapped into the account. For example: 



.. code::

  "groups-partition": {
            "salesmarketing": ["sales", "marketing"],
            "devsupport": ["engineering", "support"],
  }

Here salesmarketing and devsupport are names for the groups partition and are used as the corresponding Eucalyptus account names. 

{{% notice note %}}If you use groups-partition, remove the accounting-groups section. These two sections are mutually exclusive. {{% /notice %}}