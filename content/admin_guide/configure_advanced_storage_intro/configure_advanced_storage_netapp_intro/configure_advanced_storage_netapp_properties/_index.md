+++
title = "Configurable NetApp SAN Properties"
weight = 10
+++

This topic lists the NetApp SAN-specific properties you can configure using , along with their valid values and Eucalyptus default values.
{{% notice note %}}
The following configuration options are a subset of the Netapp SAN configuration parameters. Changing these default values may cause storage operations to fail. Please proceed at your own risk. For more information on NetApp configuration, please refer to the and the (these links require you to register and login). 
{{% /notice %}}

## 7-Mode and Cluster Mode Properties
The following table lists properties that are applicable to both 7-mode and cluster mode: 



| Eucalyptus Property | Description | Valid Values | 
|  :---- |  :---- |  :---- | 
| <region>.storage.enablespacereservation | LUN space reservation determines when space for the LUN is reserved or allocated from the flex volume. With reservations enabled the space is subtracted from the volume total when the LUN is created. If reservations are disabled, space is first taken out of the volume as writes to the LUN are performed. | Default value: true | 
| <region>.storage.enablededup | Data deduplication removes duplicate blocks, storing only unique blocks of data in the flex volume, and it creates a small amount of additional metadata in the process. It is disabled by default. <region>.storage.enablecompression must be false before disabling deduplication. | Default value: false | 
| <region>.storage.enablecompression | Data compression is a software-based solution that provides transparent data compression. It has the ability to run either as an inline process as data is written to disk or as a scheduled process. Compression is disabled by default. <region>.storage.enablededup must be true before enabling data compression. <region>.storage.enableinlinecompression must be false before disabling compression. | Default value: false | 
| <region>.storage.enableinlinecompression | When data compression is configured for inline operation, data is compressed in memory before it is written to disk. It is disabled by default. <region>.storage.enablecompression must be true before enabling inline compression. | Default value: false | 
| <region>.storage.dedupschedule | Schedule string for the dedup and or compression operation on flex volumes. <region>.storage.enablededup must be true before configuring the schedule. If the schedule is not configured, NetApp applies a default schedule to the flex volume. In Cluster-Mode, either the schedule or the policy can be configured for the flex volume. Both cannot be configured together. The format of the schedule string is: “day_list@hour_list” or “hour_list@day_list” or ”-” or “auto”. day_list specifies which days of the week the sis operation should run. It is a comma-separated list of the first three letters of the day: sun, mon, tue, wed, thu, fri, sat. Day ranges such as mon-fri can also be used. hour_list specifies which hours of the day the sis operation should run on each scheduled day. hour_list is a comma-separated list of the integers from 0 to 23. Hour ranges such as 8-17 are allowed. Step values can be used in conjunction with ranges. If ”-” is specified, no schedule is set. The “auto” schedule string means the sis operation will be triggered by the amount of new data written to the volume. | Default value: n/a | 
| <region>.storage.lunostype | The operating system of the host accessing the LUN. This determines the layout of the data on the LUN, the geometry used to access that data, and property offsets for the LUN to ensure it is properly aligned with the upper layers of the file system | Default value: linuxValid values: solaris, Solaris_efi, windows, windows_gpt, windows_2008, hpux, aix, linux, netware, xen, or hyper_v | 
| <region>.storage.initiatorostype | Operating system type of the hypervisor hosting the instances. | Default value: linux Valid values: solaris, windows, hpux, aix, linux, netware, xen, or hyper_v | 
| <region>.storage.fractionalreserve | The percentage of space reserved for overwrites of reserved objects (LUNs or files) in a volume. | 0-100; default is 0 | 
| <region>.storage.noatimeupdate | Prevents the update of inode access times when a file is read. | "on" (default) or "off" | 
| <region>.storage.tryfirst | Determines if the volume size is increased before deleting snapshots if enableautosize property is "true". | "volume_grow" (default) or "snap_delete" | 
| <region>.storage.guarantee | Controls space reservation for flexible volumes. See the NetApp SDK documentation for more information. | "none", "file", or "volume" (default) | 
| <region>.storage.enableautosize | Toggles the flex volume autosize feature. | "true" (default) or "false" | 
| <region>.storage.volautosizemaxmultiplier | Flex volume's maximum size allowed, specified as a multiple of the original size | Integer >= 1; default is 3 | 
| <region>.storage.volautosizeincrementinmb | Flex volume's increment size in megabytes. | Integer >= 1; default is 256 | 
| <region>.storage.snappercent | Additional space reserved on the flex volume to store automatic and manual snapshots created outside of Eucalyptus. The amount of space to be reserved is specified as a percentage of the flex volume. | Integer >= 0; default is 0 | 
| <region>.storage.aggregate | Aggregates that can be used to create and manage volumes and snapshots. If a list of aggregates is configured, Eucalyptus will pick one based on <region>.storage.uselargestaggregate strategy. If no aggregate is provided Eucalyptus will query the NetApp SAN for available aggregates and choose one based <region>.storage.uselargestaggregate strategy. | Comma-separated string | 
| <region>.storage.uselargestaggregate | If set to “true” Eucalyptus will pick the largest available aggregate from a list of aggregates. If set to “false” the smallest available aggregate will be chosen. | "true" (default) or "false" | 


## 7-Mode Properties
The following properties are specific to 7-mode: 



| Eucalyptus Property | Description | Valid Values | 
|  :---- |  :---- |  :---- | 
| <region>.storage.convertucode | Setting this option to "on" forces conversion of all directories to UNICODE format when accessed from both NFS and CIFS. | "on" (default) or "off" | 
| <region>.storage.createucode | Setting this option to "on" forces UNICODE format directories to be created by default from NFS and CIFS. | "on" (default) or "off" | 
| <region>.storage.snapschedweeks | Number of weekly snapshots to keep online. | Integer >= 0; default is 0 | 
| <region>.storage.snapscheddays | Number of daily snapshots to keep online. | Integer >= 0; default is 0 | 
| <region>.storage.snapschedhours | Number of hourly snapshots to keep online. | Integer >= 0; default is 0 | 
| <region>.storage.nosnap | Disable automatic snapshots. If set to “true”, snapshot scheduling properties <region>.storage.snapschedweeks and <region>.storage.snapscheddays and <region>.storage.snapschedhours are ignored, and the SC transmits the default value (0) in their place to the NetApp SAN. | "true" (default) or "false" | 


## Cluster Mode Properties
The following properties are cluster mode specific: 



| Eucalyptus Property | Description | Valid Values | 
|  :---- |  :---- |  :---- | 
| <region>.storage.snapshotpolicy | Snapshot retention policy determines how long the scheduled snapshots in the reserve are kept before being deleted automatically. This applies to automatic snapshots only. | String; default is "none" | 
| <region>.storage.autosnapshots | Disable automatic snapshots. If set to “false” snapshot scheduling policy defined by <region>.storage.snapshotpolicy is ignored and SC transmits the default value (“none”) in its place to the NetApp SAN. | "true" (default) or "false" | 
| <region>.storage.deduppolicy | Name of the sis policy to be attached to flex volumes in cluster-mode. <region>.storage.enablededup must be true before configuring the policy. Either the schedule or the policy can be configured for the flex volume. Both cannot be configured together. | Default value: n/a | 
| <region>.storage.portset | Name of the portset to bind to an igroup in cluster-mode. Port sets are collections of iSCSI ports/LIFs. A port set can be used to restrict access to the LUN by making it visible only through target ports that are contained in the port set definition. | Default value: n/a | 

