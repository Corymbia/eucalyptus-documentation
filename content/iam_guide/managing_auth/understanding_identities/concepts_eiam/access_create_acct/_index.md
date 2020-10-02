+++
title = "Account Creation"
weight = 10
+++

This topic describes the process for creating an account using the command line tool.You must be a cloud administrator to use this command. Accounts created are available for immediate access. 

To create an account, run the following command: 


    euare-accountcreate -a account_name

When an account is created by `euare-accountcreate` command, an "admin" user is created by default. 
{{% notice note %}}
Note the following security considerations of the "admin" user when an account is initially created: 
{{% /notice %}}



{{% notice note %}}
Eucalyptus has discontinued account registration status retrieval, however, for compatibility with older versions of Eucalyptus, the ability to view and manipulate registration status is limited to the system administrator through Euca2ools. For more information about the command line tools, see the . 
{{% /notice %}}
