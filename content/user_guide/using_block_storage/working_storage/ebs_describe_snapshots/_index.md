+++
title = "List Available Snapshots"
weight = 50
+++

You can use the Eucalyptus command line tools to list available snapshots and retrieve information about a specific snapshot. 

To get a list of all available snapshots in your Eucalyptus cloud, enter the following command: 

    euca-describe-snapshots

To get information about one specific snapshot, use the `euca-describe-snapshots` command and specify the snapshot ID. 

    euca-describe-snapshots snap-00000000

