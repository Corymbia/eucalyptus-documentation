+++
title = "Imaging Worker"
weight = 10
+++

This topic contains troubleshooting tips for the Imaging Worker.Some requests that require the Imaging Worker might remain in pending for a long time. For example: an import task or a paravirtual instance run. If request remains in pending, the Imaging Worker instance might not able to run because of a lack of resources (for example, instance slots or IP addresses). 

You can check for this scenario by listing latest AutoScaling activities: 



    euscale-describe-scaling-activities -g asg-euca-internal-imaging-worker-01

Check for failures that indicate inadequate resources such as: 



    ACTIVITY        1950c4e5-0db9-4b80-ad3b-5c7c59d9c82e    2014-08-12T21:05:32.699Z        asg-euca-internal-imaging-worker-01    Failed   Not enough resources available: addresses; please stop or terminate unwanted instances or release unassociated elastic IPs and try again, or run with private addressing only

