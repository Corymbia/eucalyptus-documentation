+++
title = "Special User Attributes"
weight = 5
+++

..  _access_special:

Eucalyptus extends the IAM model by providing the following extra attributes for a user.

* This is only meaningful for the account administrator (that is, the account level). 

* . Use this attribute to temporarily disable a user. 

* 

* Add any name-value pair to a user’s custom information attribute. This is useful for attaching pure text information, like an address, phone number, or department. This is especially helpful with external LDAP or Active Directory services. 

You can retrieve and modify the registration status, enabled status, and password expiration date using the ``euare-usergetattributes`` and ``euare-usermod`` commands. You can retrieve and modify custom information using ``euare-usergetinfo`` and ``euare-userupdateinfo`` commands. For more information, see the `Euca2ools Reference Guide <../euca2ools-guide/index.dita>`_ for details about these commands. 

