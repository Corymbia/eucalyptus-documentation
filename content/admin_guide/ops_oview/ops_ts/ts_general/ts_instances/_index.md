+++
title = "Instances"
weight = 10
+++

This topic contains information to help you troubleshoot your instances.
Inaccurate IP addresses display in the output of euca-describe-addresses.
 This can occur if you add IPs from the wrong subnet into your public IP pool, do a restart on the CC, swap out the wrong ones for the right ones, and do another restart on the CC. To resolve this issue, run the following commands. 


{{% notice note %}}
A restart should only be performed when no instances are running, or when instance service interruption can be tolerated. A restart causes the CC to reset its networking configuration, regardless of whether or not it is in use. 
{{% /notice %}}

    systemctl stop eucalyptus-cloud.service
    systemctl stop eucalyptus-cluster.service
    iptables -F
    systemctl restart eucalyptus-cluster.service
    systemctl start eucalyptus-cloud.service


NC does not recalculate disk size correctly
 This can occur when trying to add extra disk space for instance ephemeral storage. To resolve this, you need to delete the instance cache and restart the NC. 

For example: 


    rm -rf /var/lib/eucalyptus/instances/* 
    systemctl restart eucalyptus-node.service               				


