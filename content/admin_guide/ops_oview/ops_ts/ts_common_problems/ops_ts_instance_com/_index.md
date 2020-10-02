+++
title = "Problem: can't communicate with instance"
weight = 10
+++

Use ping from a client (not the CLC). Can you ping it? 

Yes: Check the open ports on security groups and retry connection using SSH or HTTP. Can you connect now? Yes. Okay, then. You're work is done. No: Try the same procedure as if you can't ping it up front. No: Is your cloud running in Edge networking mode? 

* Yes: Run `euca-describe-nodes` . Is your instance there? 


* No, it is not in Edge networking mode: 
