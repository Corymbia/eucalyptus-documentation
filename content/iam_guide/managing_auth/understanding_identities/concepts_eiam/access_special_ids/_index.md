+++
title = "Special Identities"
weight = 20
+++

Eucalyptus has two special identities for the convenience of administration and use of the system.

* The account: Each user in the eucalyptus account has unrestricted access to all of the cloud's resources, similar to the superuser on a typical Linux system. These users are often referred to as system administrators or cloud administrators. This account is automatically created when the system starts for the first time. You cannot remove the eucalyptus account from the system. 
* The user of an account: Each account, including the eucalyptus account, has a user named admin. This user is created automatically by the system when an account is created. The admin of an account has full access to the resources owned by the account. You can not remove the admin user from an account. The admin can delegate resource access to other users in the account by using policies. 
