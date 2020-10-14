+++
title = "Start the CC"
weight = 40
+++

**Prerequisites** 

You should have installed and configured Eucalyptus before starting the CC. 

**To start the CC** 

Log in to the Cluster Controller (CC) host machine. If you want the CC service to start at each boot-time, run this command: 

    systemctl enable eucalyptus-cluster.service

Enter the following command to start the CC: 

    systemctl start eucalyptus-cluster.service

If you have a multi-zone setup, repeat this step on the CC in each zone. 
