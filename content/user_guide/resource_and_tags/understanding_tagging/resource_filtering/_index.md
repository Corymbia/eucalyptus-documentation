+++
title = "Filtering Resources"
weight = 20
+++

You can search and filter resources based on the tags you use. For example, you can list a Eucalyptus Machine Image (EMI) using euca-describe-images, and you can list instances using euca-describe-instances .

## Filtering Overview
Results from describe commands can be long. Use a filter to include only the resources that match certain criteria. For example, you can filter so that a returned list shows only the EMIs that use an EBS volume as the root device volumes. 

Filtering also allows you to:

* Specify multiple filter values: For example, you can list all the instances whose type is either m1.small or m1.large.
* Specify multiple filters: for example, you can list all the instances whose type is either m1.small or m1.large, and that have an attached EBS volume that is set to delete when the instance terminates.
* Use wildcards with values: For example, you can use *production* as a filter value to get all EBS snapshots that include production in the description.

In each case, the instance must match all your filters to be included in the results. Filter values are case sensitive.

