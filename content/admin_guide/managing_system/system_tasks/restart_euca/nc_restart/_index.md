+++
title = "Restart an NC"
weight = 60
+++

To restart an NC perform the steps listed in this topic.Log in to the NC and enter the following command: 

    systemctl restart eucalyptus-node.service

Repeat for each NC. Verify that the following is even needed. If so, replicate for other NC-tasks. You can automate the restart command for all of your NCs. Store a list of your NCs in a file called *nc-hosts* that looks like: 

    nc-host-00
    nc-host-01
    ...
    nc-host-nn

To restart all of your NCs, run the following command: 

    cat nc-hosts | xargs -i ssh root@{} systemctl restart eucalyptus-node.service

