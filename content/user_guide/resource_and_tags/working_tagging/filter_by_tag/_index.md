+++
title = "Filter by Tag"
weight = 50
+++

You can describe your resources and filter the results based on the tags. To filter by tag: 

Enter the following command and parameter: 

    euca-describe-tags --filter resource-type=[resource_type]

The following example describes all your tags. 

    euca-describe-tags
    TAG  emi-1A2B3C4D  image  appserver
    TAG  emi-1A2B3C4D  image  stack  dev
    TAG  i-5F4E3D2A  instance  appserver
    TAG  i-5F4E3D2A  instance  stack  dev
    TAG  i-12345678  instance  database_server
    TAG  i-12345678  instance  stack  test

The following example describes the tags for a resource with ID emi-1A2B3C4D. 

    euca-describe-tags --filter "resource-id=emi-1A2B3C4D"
    TAG  emi-1A2B3C4D  image  appserver
    TAG  emi-1A2B3C4D  image  stack  dev

The following example describes the tags for all your instances. 

    euca-describe-tags --filter "resource-type=instance"
    TAG  i-5F4E3D2A  instance  appserver
    TAG  i-5F4E3D2A  instance  stack  dev
    TAG  i-12345678  instance  database_server
    TAG  i-12345678  instance  stack  test

