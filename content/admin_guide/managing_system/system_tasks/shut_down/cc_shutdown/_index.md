+++
title = "Shut Down the CCs"
weight = 10
hidden = true
+++

To shut down the CCs: 

Log in as root to a machine hosting a CC. Enter the following command: 
    systemctl stop eucalyptus-cluster.service

Repeat for each machine hosting a CC. 