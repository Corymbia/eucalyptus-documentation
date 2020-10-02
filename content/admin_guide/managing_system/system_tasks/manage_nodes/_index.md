+++
title = "Migrate Instances Between Node Controllers"
weight = 10
+++

In order to ensure optimal system performance, or to perform system maintenance, it is sometimes necessary to move running instances between Node Controllers (NCs). You can migrate instances individually, or migrate all instances from a given NC.
{{% notice note %}}
For migrations to succeed, you must have set to the same value in the file on each NC. 
{{% /notice %}}
To migrate a single instance to another NC, enter the following command: 
    euserv-migrate-instances -i INSTANCE_ID

You can also optionally specify `--include-dest HOST_NC_IP` or `--exclude-dest HOST_NC_IP` , to ensure that the instance is migrated to one of the specified NCs, or to avoid migrating the instance to any of the specified NCs. These flags may be used more than once to specify multiple NCs. 

To migrate all instances away from an NC, enter the following command: 
    euserv-migrate-instances --source HOST_NC_IP

You can also optionally specify `euserv-modify-service -s stop HOST_NC_IP` , to stop the specified NC and ensure that no new instances are started on that NC while the migration occurs. This allows you to safely remove the NC without interrupting running instances. The NC will remain in the DISABLED state until it is explicitly enabled using `euserv-modify-service -s start HOST_NC_IP` . 

In some cases, timeouts may cause a migration to initially fail. Run the command again to complete the migration. 

If the migration fails, check the *nc.log* file on the source and destination NCs. If you see an error similar to: 
    libvirt: Cannot get interface MTU on 'br0': No such device (code=38)

... then ensure the NCs have the same interface and bridge device names, as described in [](../install-guide/configuring_bridge.dita#configuring_bridge) . 

