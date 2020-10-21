+++
title = "Customizing Your Deployment"
weight = 40
+++

This section describes the most commonly applied post-install customizations and the issues they pose: 

* Over-subscription 
* Networking changes (EDGE mode) 
* CloudWatch tweaks/customizations 
* Capacity changes

## Over-subscription
Over-subscription refers to the practice of expanding your computer beyond its limits. Over-subscription applies only to node controllers. You may modify disks and cores to allow enough usage buffer for your instance. Navigate to `/etc/eucalyptus/` and locate the `eucalyptus.conf` file. Edit the following values to define the appropriate size buffers for your instances: `NC_WORK_SIZE` Defines the amount of disk space available for instances to be run. Defaults to 1/3 of the currently available disk space on the NC, and NC_CACHE_SIZE defaults to the other 2/3. 

`NC_CACHE_SIZE` Defines how much disk space is needed for images to be cached. `MAX_CORES` Defines the maximum number of cores that can be provided to VMs on each NC. If it is 0 or not present, then the only limit on the number of instances is the number of cores available on the NC. If it is present, any value greater than 256 is treated as 256. In order for these changes to take effect, you must restart the NC. 


## Networking Changes (EDGE modes)
You can modify the default by adding network IPs to your cloud. Adding public IPs does not require shutting down the whole system.

To add network IPs:In EDGE mode, adding or changing the IP involves creating a JSON file and uploading it the Cloud Controller (CLC). See [Configure for Edge Mode]({{< ref nw_edge.md >}}) for more details. No restart needed, changes apply automatically. 


## Change CloudWatch Properties
You can change the following CloudWatch properties:

| Property | Description | 
|  :---- |  :---- | 
| cloud.monitor.default_poll_interval_mins | This is how often the CLC sends a request to the CC for sensor data. Default value is 5 minutes. If you set it to 0 = no reporting. The more often you poll, the more hit on system performance. | 
| cloud.monitor.history_size | This is how many data value samples are sent in each sensor data request. The default value is 5. How many samples per poll interval. | 
| cloudwatch.enable_cloudwatch_service | Disables CloudWatch when set to false. | 


## Change Capacity
Capacity changes refer to adding another zone or more nodes. To add another zone, [install]({{< ref install_repos_intro.md >}}) , [start]({{< ref starting_euca.md >}}) , and [register]({{< ref registering_ccs.md >}}) . To add more nodes, see [Add a Node Controller]({{< ref add_nodes.md >}}) . 
