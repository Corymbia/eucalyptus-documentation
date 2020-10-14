+++
title = "Testing Your Deployment"
weight = 30
+++

This topic details what you should test when you want to make sure your deployment is working. The following suggested test plan contains tasks that ensure DNS, imaging, and storage are working.
## DNS


* Verify that instances can ping their: 
* Verify that instances are pingable on their public DNS names from: 

## Imaging


* Verify that an EBS-backed image boots successfully 
* Verify that you can create an image from a running EBS-backed instance 
* Verify that you can install a new Ubuntu image 
* Verify that you can deregister an image 
* Verify that you can import an instance 
* Verify that you can import a volume 

## Walrus


* Verify that you can make a basic s3cmd request 
* Verify that you can successfully perform a multi-part upload (use a 1G+ file) 
