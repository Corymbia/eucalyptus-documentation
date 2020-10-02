+++
title = "Restore the Database"
weight = 5
+++

To restore the cloud database follow the steps listed in this topic.
{{% notice note %}}
Sometimes you'll get this message on both startup and shutdown of the database: ... where is actually your current directory, meaning if you run the command from , then the path in the output will be instead of . The message is completely benign and can be ignored. 
{{% /notice %}}
**To restore the database** 

Stop the CLC service. 
    systemctl stop eucalyptus-cloud.service

Remove traces of the old database. 
    rm -rf /var/lib/eucalyptus/db

Restore the cloud security credentials in the keys directory. 
    tar -xvf ~/eucalyptus-keydir.tgz -C /

Re-initialize the database structure. 
    clcadmin-initialize-cloud

Start the database manually. 
    su eucalyptus -s /bin/bash -c "/usr/bin/pg_ctl start -w \
    -s -D/var/lib/eucalyptus/db/data -o '-h0.0.0.0/0 -p8777 -i'"

Restore the backup. 
    psql -U root -d postgres -p 8777 -h /var/lib/eucalyptus/db/data -f/root/eucalyptus_pg_dumpall-backup.sql

Stop the database manually. 
    su eucalyptus -s /bin/bash -c "/usr/bin/pg_ctl stop -D/var/lib/eucalyptus/db/data"

Start CLC service 
{{% notice note %}}
If you are upgrading, skip this step (you don't want to start the CLC service now because you haven't restored the rest of the cloud data yet; starting the CLC appears in the installation steps, later). 
{{% /notice %}}

    systemctl start eucalyptus-cloud.service

