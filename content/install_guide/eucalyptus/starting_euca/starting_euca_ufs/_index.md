+++
title = "Start the UFS"
weight = 20
+++

**Prerequisites** You should have installed and configured Eucalyptus before starting the UFS. 

**To start the UFS** 

Log in to the User-Facing Services (UFS) host machine. If you want the UFS service to start at each boot-time, run this command: 

    systemctl enable eucalyptus-cloud.service

Enter the following command to start the UFS: 

    systemctl start eucalyptus-cloud.service

Repeat for each UFS host machine. 
