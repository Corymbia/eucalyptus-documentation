+++
title = "Synchronize Components"
weight = 10
+++

To synchronize your Eucalyptus component machines with an NTP server, perform the following tasks. 

Enter the following command on a machine hosting a Eucalyptus component: 

    # ntpdate pool.ntp.org
    # systemctl start ntpd.service
    # systemctl enable ntpd.service
    # ps ax | grep ntp
    # hwclock --systohc  

Repeat for each machine hosting a Eucalyptus component. 