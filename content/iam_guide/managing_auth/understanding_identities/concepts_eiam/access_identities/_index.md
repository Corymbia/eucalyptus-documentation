+++
title = "User Identities"
weight = 10
+++

In Eucalyptus, user identities are organized into accounts. An account is the unit of resource usage accounting, and also a separate namespace for many resources (security groups, key pairs, users, etc.).Accounts are identified by either a unique ID (UUID) or a unique name. The account name is like IAM’s account alias. It is used to manipulate accounts. However, for AWS compatibility, the EC2 commands often use account ID to display resource ownership. 

There are command line tools to discover the correspondence of account ID and account name. For example, euare-accountlist lists all the accounts with both their IDs and names. 

An account can have multiple users, but a user can only be in one account. Within an account, users can be associated with Groups. Group is used to attach access permissions to multiple users. A user can be associated with multiple groups. Because an account is a separate name space, user names and group names have to be unique only within an account. Therefore, user X in account A and user X in account B are two different identities. 

Both users and groups are identified by their names, which are unique within an account (they also have UUIDs, but are rarely used). 

