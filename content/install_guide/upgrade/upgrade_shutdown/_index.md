+++
title = "Shutdown Services"
weight = 10
+++

This topic describes how to stop all Eucalyptus services.**Prerequisites** See [](upgrade_prep.dita#upgrade_prep) for the complete list of upgrade prerequisites. 

The steps you take depend upon where Eucalyptus services are hosted. 

**To shut down Eucalyptus services** 

Log in to the CLC host machine and shut down the CLC service: 
    systemctl stop eucalyptus-cloud.service

If you have separate SC host machines, log in to each host and shut down the SC services: 
    systemctl stop eucalyptus-cloud.service

If you have a separate Walrus host machine, log in and shut down the Walrus backend services: 
    systemctl stop eucalyptus-cloud.service

If you have separate UFS host machines, log in to each host and shut down the UFS services: 
    systemctl stop eucalyptus-cloud.service

If there are any other Eucalyptus services (for example Walrus, SC, UFS) co-located on the CC host machine, use this command to shut down the other services on the CC host, and in the correct order: 
    systemctl stop eucalyptus-cloud.service

Log in to each CC host machine and shut down the CC service: 
    systemctl stop eucalyptus-cluster.service

(Optional) If you are not sure which hosts are *running* eucanetd, check the status on each CLC, CC, and NC: 
    systemctl status eucanetd.service


{{% notice note %}}
Depending on your network configuration, eucanetd might be running on any of these hosts. Also note that it can be and not . See for more information. 
{{% /notice %}}
Make note of all hosts that have eucanetd *running* ; you'll need this when you [start up the services](upgrade_start.dita#upgrade_start) again. 

Log in to each host machine running eucanetd and shut it down: 
    systemctl stop eucanetd.service

Log in to each NC host machine and shut down the NC service: 
    systemctl stop eucalyptus-node.service


{{% notice note %}}
Running instances on the NC will continue running. For more information see . 
{{% /notice %}}
Log in to each Management Console host machine and shut down the console service: 
    systemctl stop eucaconsole.service

You are now ready to [](upgrade_euca2ools_packages.dita) . 