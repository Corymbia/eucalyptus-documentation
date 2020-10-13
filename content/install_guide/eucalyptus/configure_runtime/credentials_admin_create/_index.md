+++
title = "Create the Eucalyptus Cloud Administrator User"
weight = 20
+++

After your cloud is running and DNS is functional, create a user and access key for day-to-day cloud administration.**Prerequisites** 

* cloud services must be installed and registered. 
* DNS must be configured. 

{{% notice note %}}
This is where you would begin using the admin role, if you want to use that feature. 
{{% /notice %}}
**To create a cloud admin user** Eucalyptus admin tools and Euca2ools commands need configuration from *~/.euca* . If the directory does not yet exist, create it: 

    mkdir ~/.euca

Choose a name for the new user and create it along with an access key: 

    euare-usercreate -wld DOMAIN USER >~/.euca/FILE.ini

where: 

* must match the DNS domain chosen in . 
* is the name of the new admin user. 
* can be anything; we recommend a descriptive name that includes the user's name. 


This creates a file with a region name that matches that of your cloud's DNS domain; you can edit the file to change the region name if needed. 

Need to sync up the various credential-related topics, across the doc set. Might want to make the IAM XREF more specific at that time. DOC-1987 improvement suggestion from Garrett for the Admin Guide and would be an XREF from this topic, as a suggested alternative admin role. 
{{% notice note %}}
This creates an admin user in the built-in 'eucalyptus' account. The admin user has full control of all aspects of the cloud. For additional security, you might instead want to create a new account and grant it access to a more limited administration role. See the for more information. 
{{% /notice %}}
Switch to the new admin user: 

    eval `euare-releaserole`
    export AWS_DEFAULT_REGION=REGION

where: 

* must match the region name from the previous step. By default, this is the same as the cloud's DNS domain chosen in . 


As long as this file exists in *~/.euca* , you can use it by repeating the `export` command above. These `euca2ools.ini` configuration files are a flexible means of managing cloud regions and users.

**What to do next** 

The remainder of this guide assumes you have completed the above steps. 

Use these credentials after this point. 

