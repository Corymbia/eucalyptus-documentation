+++
title = "Problem: instance runs but fails"
weight = 10
+++

Run `euca-describe-nodes` to verify if instance is there. Is the instance there? 

Yes: Go to the [NC log]({{< ref ts_logs.md >}}) for that NC and grep your instance ID. Did you find the instance? 

* Yes: Is there an error message? 


No: Go to the [CC log]({{< ref ts_logs.md >}}) and grep the instance ID. Is it there error message? 

* Yes: The error message should give you some helpful information. 


* No: grep the instance ID in [cloud-output.log]({{< ref ts_logs.md >}}) . Is there error message? 


No: Log in as admin and run `euca-describe-instance` . Is the instance there? 

* Yes: 
* No: Start over and run a new instance, recreate failure, and start these steps over. 


