+++
title = "Create Credentials"
weight = 10
+++

The first time you get credentials using the Eucalyptus Administrator Console, a new secret access key is generated. On each subsequent request to get credentials, an existing active secret Key is returned. You can also generate new keys using the command.
{{% notice note %}}
Each request to get a user's credentials generates a new pair of a private key and X.509 certificate. 
{{% /notice %}}
To generate a new key for a user by an account administrator, enter the following 
    euare-useraddkey USERNAME

To generate a private key and an X.509 certificate pair, enter the following: 
    euare-usercreatecert USERNAME

