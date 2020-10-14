+++
title = "Plan Your Hardware"
weight = 20
+++

This topic describes ways you can install Eucalyptus services on your physical servers.You can run Eucalyptus services in any combination on the various physical servers in a data center. For example, you can install the Cloud Controller (CLC), Walrus, CC, and SC on one host machine, and NCs on one or more host machines. Or you can install each service on an independent physical server. This gives each service its own local resources to work with. 

Often in installation decisions, you must trade deployment simplicity for performance. For example, if you place all cloud (CLC) and zone (CC) services on a single machine, it makes for simple administration. This is because there is only one machine to monitor and control for the Eucalyptus control services. But, each service acts as an independent web service; so if they share a single machine, the reduced physical resources available to each service might become a performance bottleneck. 

