+++
title = "Launch an Instance"
weight = 5
+++

To launch an instance: 

Use the euca-run-instances command and provide an image ID and the user data file, in the format `euca-run-instances <image_id>` . For example: 
    euca-run-instances emi-EC1410C1 

For additional details and options that can be used with the *euca-run-instances* command, For more information, see [EC2-Compatible Commands, euca-run-instances](../euca2ools-guide/euca-run-instances.dita) . Enter the following command to get the launch status of the instance: 
    euca-describe-instances <instance_id>

Need response from Eucalyptus then uncomment the para below. 