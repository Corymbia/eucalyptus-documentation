+++
title = "Troubleshooting"
weight = 5
chapter = true
+++


# Troubleshooting
This topic details how to find information you need to troubleshoot most problems in your cloud. To troubleshoot Eucalyptus, you must have the following:

* a knowledge about which machines each Eucalyptus component is installed on
* root access to each machine hosting Eucalyptus components
* an understanding of the network mode (EDGE, VPCMIDO)
* an understanding of eucanetd and the configuration connecting the Eucalyptus components

For most problems, the procedure for tracing problems is the same: start at the bottom to verify the bottom-most component, and then work your way up. If you do this, you can be assured that the base is solid. This applies to virtually all Eucalyptus components and also works for proactive, targeted monitoring. 


{{% children %}}
