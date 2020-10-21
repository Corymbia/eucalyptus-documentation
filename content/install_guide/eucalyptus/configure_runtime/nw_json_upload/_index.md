+++
title = "Upload the Network Configuration"
weight = 30
+++

This topic describes how to upload the network configuration created earlier in the installation process. To upload your networking configuration:

{{% notice note %}}
This step can only be run after getting your credentials in [Create the Eucalyptus Cloud Administrator User]({{< ref credentials_admin_create >}}). 
{{% /notice %}}

Run the following command to upload the configuration file to the CLC (with valid Eucalyptus admin credentials): 

```bash
euctl cloud.network.network_configuration=@/path/to/your/network_config_file
```

To review the existing network configuration run:

```bash
euctl  --dump --format=raw cloud.network.network_configuration
```

When you use the Ansible playbook for deployment a network configuration file is available at */etc/eucalyptus/network.yaml* on the CLC.
