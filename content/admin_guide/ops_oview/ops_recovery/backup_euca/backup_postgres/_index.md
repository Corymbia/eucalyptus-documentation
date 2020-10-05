+++
title = "Back Up the Database"
weight = 10
+++

To back up the cloud database follow the steps listed in this topic.Bucket and object metadata are stored in the Eucalyptus cloud database. **To back up the database** 

Log in to the CLC. The cloud database is on the CLC. Extract the Eucalyptus PostgreSQL database cluster into a script file. 

    pg_dumpall --oids -c -h/var/lib/eucalyptus/db/data -p8777 -U root -f/root/eucalyptus_pg_dumpall-backup.sql

Back up the cloud security credentials in the keys directory. 

    tar -czvf ~/eucalyptus-keydir.tgz /var/lib/eucalyptus/keys

