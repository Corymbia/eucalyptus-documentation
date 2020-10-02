+++
title = "Change Network Configuration"
weight = 5
chapter = true
+++


# Change Network Configuration
You might want to change the original network configuration of your cloud. To change your network configuration, perform the tasks listed in this topic.Log in to the CLC and open the */etc/eucalyptus/eucalyptus.conf* file. Navigate to the Networking Configuration section and make your edits. Save the file. Restart the Cluster Controller. 
    systemctl restart eucalyptus-cluster.service



{{% children %}}
