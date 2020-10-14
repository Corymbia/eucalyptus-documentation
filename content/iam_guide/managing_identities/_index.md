+++
title = "Manage Identities Overview"
weight = 30
+++

Like IAM, the user identities in Eucalyptus are organized into Accounts. An account is the unit of resource usage accounting, and also a separate name space for many resources, for example, security groups, key pairs, users, and so on. Unique ID (UUID) or a unique name identifies an account. The account name is equivalent to IAM’s account alias. In Eucalyptus, the account name is used to manipulate accounts in most cases. However, to be compatible with AWS, the EC2 commands often use account ID to display resource ownership. There are command line tools to discover the correspondence of account ID with the account name. For example, lists all the accounts with both their IDs and names.
![image]({{< ref "/" >}}images/iam_diagram.png)
An account can have multiple users, but a user can only be in one account. Within an account, users can be associated with Groups. A Group is used to attach access permissions to multiple users. A user can be associated with multiple groups. Because an account is a separate name space, user names and group names have to be unique only within an account. Therefore, user X in account A and user X in account B are two different identities. Both users and groups are identified by their names, which are unique within an account (they also have UUIDs, but rarely used). 

