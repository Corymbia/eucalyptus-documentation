+++
title = "Create the Eucalyptus Cloud Administrator User"
weight = 20
+++

After your cloud is running and DNS is functional, create a user and access key for day-to-day cloud administration.

## Prerequisites

* cloud services must be installed and registered. 
* DNS must be configured. 

{{% notice note %}}
This is where you would begin using the admin role, if you want to use that feature. 
{{% /notice %}}

## Create a cloud admin user

Eucalyptus admin tools and Euca2ools commands need configuration from *~/.euca* . If the directory does not yet exist, create it:

```bash
mkdir ~/.euca
```

Choose a name for the new user and create it along with an access key: 

```bash
euare-usercreate -wld DOMAIN USER >~/.euca/FILE.ini
```

where: 

* **DOMAIN** must match the DNS domain for the cloud. 
* **USER** is the name of the new admin user. 
* **FILE** can be anything; we recommend a descriptive name that includes the user's name.

This creates a file with a region name that matches that of your cloud's DNS domain; you can edit the file to change the region name if needed. 

{{% notice note %}}
This creates an admin user in the built-in **eucalyptus** account. The admin user has full control of all aspects of the cloud. For additional security, you might instead want to create a new account and grant it access to a more limited administration role.
{{% /notice %}}

Switch to the new admin user: 

```bash
# eval `clcadmin-release-credentials`
# export AWS_DEFAULT_REGION=REGION
```

where: 

* **REGION** must match the region name from the previous step. By default, this is the same as the cloud's DNS domain. 

As long as this file exists in *~/.euca* , you can use it by repeating the `export` command above. These `euca2ools.ini` configuration files are a flexible means of managing cloud regions and users.

Alternatively you can configure the default region in the **global** section of your Euca2ools configuration:

```bash
# cat ~/.euca/global.ini
[global]
default-region = REGION
```

setting the **REGION** to the one from the earlier step means you do not have to use *export* to select the region.

## User impersonation

The **eucalyptus** account can act as other accounts for administrative purposes. To act as the *admin* user in the *account-1* account run:

```bash
# eval `clcadmin-impersonate-user -a account-1 -u admin`
```

Impersonating an account allows you to view and modify resources for that account. For example, you can clean up resources in an account before deleting it.

To stop impersonating run:

```bash
clcadmin-release-credentials
```

## Next steps

The remainder of this guide assumes you have completed the above steps. 

Use these credentials after this point. 

