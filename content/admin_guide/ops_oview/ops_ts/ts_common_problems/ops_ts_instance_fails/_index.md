+++
title = "Problem: instance runs but fails"
weight = 5
+++

Run `euca-describe-nodes` to verify if instance is there. Is the instance there? 

Yes: Go to the [NC log](../troubleshooting-guide/ts_logs.dita) for that NC and grep your instance ID. Did you find the instance? 

* Yes: Is there an error message? 


No: Go to the [CC log](../troubleshooting-guide/ts_logs.dita) and grep the instance ID. Is it there error message? 

* Yes: The error message should give you some helpful information. 


* No: grep the instance ID in [cloud-output.log](../troubleshooting-guide/ts_logs.dita) . Is there error message? 


No: Log in as admin and run `euca-describe-instance` . Is the instance there? 

* Yes: 
* No: Start over and run a new instance, recreate failure, and start these steps over. 


