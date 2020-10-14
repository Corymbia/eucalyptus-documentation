+++
title = "Add a Tag"
weight = 10
+++

Use the euca-create-tags command to add a tag to a resource. 

Enter the following command and parameters: 

    euca-create-tags [resource_id] --tag [tag_key]=[tag_value]

Eucalyptus returns a the resource identifier and its tag key and value. The following example shows how to add a tag to an EMI. This tag key is `dataserver` and has no value. 

    euca-create-tags emi-1A2B3C4D --tag dataserver 
    TAG  emi-1a2b3c4d  image  dataserver

The following example shows how to add the same two tags to both an EMI and an instance. One tag key is dataserver, which has no value, an empty string. The other tag key is stack, which has a value of `Production` . 

    euca-create-tags emi-1A2B3C4D i-6F5D4E3A --tag dataserver --tag stack=Production
    TAG  emi-1A2B3C4D  image  dataserver
    TAG  emi-1A2B3C4D  image  stack  Production
    TAG  i-6F5D4E3A  image  dataserver
    TAG  i-6F5D4E3A  image  stack  Production

