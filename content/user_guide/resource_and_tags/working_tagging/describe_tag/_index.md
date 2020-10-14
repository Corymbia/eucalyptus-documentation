+++
title = "List Tags"
weight = 20
+++

Use the euca-describe-tags command to list your tags and filter the results different ways. 

Enter the following command and parameters: 

    euca-describe-tags --filter resource-type=[resource_type]" --filter
    "key=[key_name]" --filter "value=[key_value]"

The following example describes all the tags belonging to your account. 

    euca-describe-tags
    TAG  emi-1A2B3C4D  image  database_server
    TAG  emi-1A2B3C4D  image  stack  Production
    TAG  i-5F4E3D2A  instance  database_server
    TAG  i-5F4E3D2A  instance  stack  Production
    TAG  i-12345678  instance  webserver
    TAG  i-12345678  instance  stack  Test

The following example describes the tags for the resource with ID emi-1A2B3C4D. 

    ec2-describe-tags --filter "resource-id=emi-1A2B3C4D"
    TAG  emi-1A2B3C4D  image  database_server
    TAG  emi-1A2B3C4D  image  stack  Production

The following example describes the tags for all your instances. 

    ec2-describe-tags --filter "resource-type=instance"
    TAG  i-5F4E3D2A  instance  database_server
    TAG  i-5F4E3D2A  instance  stack  Production
    TAG  i-12345678  instance  webserver
    TAG  i-12345678  instance  stack  Test

The following example describes the tags for all your instances that have a tag with the key webserver. 

    ec2-describe-tags --filter "resource-type=instance" --filter "key=database_server"
    TAG  i-5F4E3D2A  instance  database_server

The following example describes the tags for all your instances that have a tag with the key stack that has a value of either Test or Production. 

    ec2-describe-tags --filter "resource-type=instance" --filter "key=stack" 
    --filter "value=Test" --filter "value=Production"
    TAG  i-5F4E3D2A  instance  stack  Production
    TAG  i-12345678  instance  stack  Test

The following example describes the tags for all your instances that have a tag with the key Purpose that has no value. 

    ec2-describe-tags --filter "resource-type=instance" --filter "key=Purpose" --filter "value="

