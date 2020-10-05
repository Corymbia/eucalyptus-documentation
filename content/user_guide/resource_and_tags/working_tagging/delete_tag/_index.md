+++
title = "Delete a Tag"
weight = 10
+++

To delete a tag: 

Enter the following command and parameters: 

    euca-delete-tags resource_id [resource_id]" --tag
    "key=[key_value]" --tag "value=[key_value]"


{{% notice note %}}
If you specify a value, the tag is deleted only if its value matches the one you specified. If you specify an empty string as the value, the tag is deleted only if the tag's value is an empty string. 
{{% /notice %}}
Eucalyptus does not return a message. The following example deletes two tags assigned to an EMI and an instance: 



    euca-delete-tags emi-1A2B3C4D i-6F5D4E3A --tag appserver --tag stack

The following example deletes a tag only if the value is an empty string: 



    euca-delete-tags snap-1A2B3C4D --tag Owner=

