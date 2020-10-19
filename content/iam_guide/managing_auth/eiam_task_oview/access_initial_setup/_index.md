+++
title = "Use Case: Create an Administrator"
weight = 10
+++

This use case details tasks for creating an administrator. These tasks require that you have your account credentials for sending requests to Eucalyptus using the command line interface (CLI) tools. To create an administrator account, perform the following tasks.


## Create an Admin Group
Eucalyptus recommends using account credentials as little as possible. You can avoid using account credentials by creating a group of users with administrative privileges. 

Create a group called administrators. 

    euare-groupcreate -g administrators

Verify that the group was created. 

    euare-grouplistbypath

Eucalyptus returns a listing of the groups that have been created, as in the following example. 

    arn:aws:iam::123456789012:group/administrators

## Add a Policy to the Group
Add a policy to the administrators group that allows its members to perform all actions in Eucalyptus. 

Enter the following command to create a policy called `admin-root` that grants all actions on all resources to all users in the administrators group: 

    euare-groupaddpolicy -p admin-root -g administrators -e Allow -a "*" -r "*" -o

## Create an Administrative User
Create a user for day-to-day administrative work and add that user to the administrators group. 

Eucalyptus admin tools and Euca2ools commands need configuration from *~/.euca* . If the directory does not yet exist, create it: 

    mkdir ~/.euca

Create an administrative user, for example alice and create it along with an access key: 

    euare-usercreate -wd DOMAIN USER >~/.euca/FILE.ini

where: 

* means output access keys and region information in a euca2ools.ini type configuration file. 
* **DOMAIN** is the DNS domain to use for region information in configuration file output (default: based on IAM URL). 
* **USER** is the name of the new admin user: alice. 
* **FILE** can be anything; we recommend a descriptive name that includes the user's name; for example:

    euare-usercreate -wd DNS_DOMAIN alice >~/.euca/alice.ini

This creates a user admin file with a region name that matches that of your cloud's DNS domain. 

Add the new admin user to the administrators group. 

    euare-groupadduser -u alice administrators

To list the new user's access keys: 

    euare-userlistkeys --region alice@DNS_DOMAIN


