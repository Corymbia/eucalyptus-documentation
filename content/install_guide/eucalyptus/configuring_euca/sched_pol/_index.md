+++
title = "Create Scheduling Policy"
weight = 30
+++

This topic describes how to set up the Cluster Controller (CC) to choose which Node Controller (NC) to run each new instance.In the CC, open the */etc/eucalyptus/eucalyptus.conf* file. In the `SCHEDPOLICY=` parameter, set the value to one of the following: `GREEDY` When the CC receives a new instance run request, it runs the instance on the first NC in an ordered list of NCs that has capacity to run the instance. At partial capacity with some amount of churn, this policy generally results in a steady state over time where some nodes are running many instances, and some nodes are running few or no instances. `ROUNDROBIN` (Default) When the CC receives a new instance run request, it runs the instance on the next NC in an ordered list of NCs that has capacity. The next NC is determined by the last NC to have received an instance. At partial capacity with some amount of churn, this policy generally results in a steady state over time where instances are more evenly distributed across the set of NCs. Save the file. 
