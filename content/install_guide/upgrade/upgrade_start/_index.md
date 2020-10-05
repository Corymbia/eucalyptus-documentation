+++
title = "Start Eucalyptus Services"
weight = 10
+++

This topic describes how to start all Eucalyptus services after upgrade.**Prerequisites** You should have successfully completed [Upgrade  Package Repositories]({{< ref upgrade_packages.md >}}) before you begin this process. 

You need to start all Eucalyptus services after upgrade. The steps you take depend upon where Eucalyptus services are hosted. 

**To start Eucalyptus services after the upgrade** 

Log in to the CLC host machine and start the services: 

    systemctl start eucalyptus-cloud.service

If you have separate SC host machines, log in to each host and start the services: 

    systemctl start eucalyptus-cloud.service

If you have a separate Walrus host machine, log in and start the services: 

    systemctl start eucalyptus-cloud.service

If you have separate UFS host machines, log in to each host and start the services: 

    systemctl start eucalyptus-cloud.service

If there are any other Eucalyptus services (for example Walrus, SC, UFS) co-located on the CC host machine, use this command to start the other services on the CC host, and in the correct order: 

    systemctl start eucalyptus-cloud.service

Log in to each CC host machine and start the service: 

    systemctl start eucalyptus-cluster.service

Log in to each NC server and start the service: 

    systemctl start eucalyptus-node.service

Log in to each host machine that was running eucanetd prior to upgrade and start the service again: 
{{% notice note %}}
Depending on your network configuration, eucanetd might have been running on any of these hosts: CLC, CC, NC. Also note that it might have been and not . See for more information. 
{{% /notice %}}




    systemctl start eucanetd.service




{{% notice note %}}
Use the list of eucanetd hosts, which you created in . 
{{% /notice %}}
You are now ready to [Verify the Services]({{< ref upgrade_verify.md >}}) . 