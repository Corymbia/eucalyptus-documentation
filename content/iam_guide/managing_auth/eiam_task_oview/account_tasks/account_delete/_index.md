+++
title = "Delete an Account"
weight = 5
+++

To delete an account perform the steps listed in this topic.
{{% notice note %}}
If there are resources tied to the account that you delete, the resources remain. We recommend that you delete these resources first. 
{{% /notice %}}
Enter the following command: 
    euare-accountdel -a <account_name> -r true

Use the `-r` option set to `true` to delete the account recursively. You don't have to use this option if have already deleted users, keys, and passwords in this account. 

Eucalyptus does not return any message. 