+++
title = "Upload the Network JSON Configuration File"
weight = 30
+++

This topic describes how to upload the JSON network configuration file you created earlier in the installation process.To upload the JSON file with your networking configuration: 


{{% notice note %}}
This step can only be run after getting your credentials in . 
{{% /notice %}}
Run the following command to upload the configuration file to the CLC (with valid Eucalyptus admin credentials): 

    euctl cloud.network.network_configuration=@/path/to/your/network_json_config_file

