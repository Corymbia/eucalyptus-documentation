+++
title = "Reporting Best Practices"
weight = 10
hidden = true
+++

This topic provides guidelines for using the reporting feature in Eucalyptus.

* Eucalyptus recommends that you run reports from the data warehouse. The Cloud Controller (CLC) generates the data. The data warehouse is a store of the stale data exported from the CLC. 
* Monitor the rate of information collected and written to the CLC database. The database expands through usage and event-driven records. More report information stored in the CLC database lessens the effectiveness of the CLC to perform its cloud duties. If the database gets too large, export the data to the data warehouse then delete the data from the CLC. 
* Be careful about deleting data in the CLC. If you delete data in the CLC after you export it, you should use the data warehouse to generate all future reports. This ensures that you have a comprehensive picture of your cloud data. 
* You can't import data from different clouds into the same data warehouse. 
