+++
title = "Start Walrus"
weight = 30
+++

**Prerequisites** 

You should have installed and configured Eucalyptus before starting the Walrus Backend. 

{{% notice note %}}
If you not using Walrus as your object storage backend, or if you installed Walrus on the same host as the CLC, you can skip this. 
{{% /notice %}}

**To start the Walrus** 

If you want the Walrus Backend service to start at each boot-time, run this command: 

    systemctl enable eucalyptus-cloud.service

Log in to the Walrus Backend host machine and enter the following command: 

    systemctl start eucalyptus-cloud.service

