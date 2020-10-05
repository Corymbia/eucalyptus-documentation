+++
title = "Tagging Resources"
weight = 10
+++

To help you manage your cloud's instances, images, and other Eucalyptus resources, you can assign your own metadata to each resource in the form of tags. You can use tags to create user-friendly names, make resource searching easier, and improve coordination between multiple users. This section describes tags and how to create them. 


## Tagging Overview
A tag consists of a key and an optional value for that key. You define both the key and the value for each tag. For example, you can define a tag for your instances that helps you track each instance's owner and stack level. 

Tags let you categorize your cloud resources in various ways. For example, you can tag resources based on their purpose, their owner, or their environment. We recommend that you devise a set of tag keys that meets your needs for each resource type. Using a consistent set of tag keys makes it easier for you to manage your resources. You can search and filter the resources based on the tags you add. For more information about filtering, see [Filtering Resources]({{< ref resource_filtering.md >}}) . 

Eucalyptus doesn't apply any semantic meaning to your tags. Instead, Eucalyptus interprets your tags simply as strings of characters. Eucalyptus doesn't automatically assign any tags on resources. 

You can only assign tags to resources that already exist. However, if you use the Management Console, you can add tags when you launch an instance. If you add a tag that has the same key as an existing tag on that resource, the new value overwrites the old value. You can edit tag keys and values, and you can remove tags from a resource at any time. You can set a tag's value to the empty string, but you can't set a tag's value to null. 


## Tagging Restrictions
The following restrictions apply to tags: 



| Restriction | Description | 
|  :---- |  :---- | 
| Maximum number of tags per resource | 10 | 
| Maximum key length | 128 Unicode characters | 
| Maximum value length | 256 Unicode characters | 
| Unavailable prefixes | You can't use either euca: or aws: as a prefix to either a tag name or value. These are reserved by Eucalyptus. | 
| Case sensitivity | Tag keys and values are case sensitive. | 

You can't terminate, stop, or delete a resource based solely on its tags. You must specify the resource identifier. For example, to delete snapshots that you tagged with a tag key called `temporary` , you must first get a list of those snapshots using euca-describe-snapshots with a filter that specifies the tag. Then you use euca-delete-snapshots with the IDs of the snapshots (for example, snap-1A2B3C4D). You can't call euca-delete-snapshots with a filter that specified the tag. For more information about using filters when listing your resources, see [Filtering Resources]({{< ref resource_filtering.md >}}) . 


## Available Resources
You can tag the following cloud resources: 



* Images (EMIs, kernels, RAM disks) 
* Instances 
* Volumes 
* Snapshots 
* Security Groups 
You can't tag the following cloud resources: 



* Elastic IP addresses 
* Key pairs 
* Placement groups 
You can tag public or shared resources, but the tags you assign are available only to your account and not to the other accounts sharing the resource. 


## 
