+++
title = "AWS CLI Installation"
weight = 10
+++

The AWS CLI is the official client for AWS. The CentOS and RHEL 7 official repositories provide a packaged AWS CLI version 1 that works well with Eucalyptus. 

To allow easy use of the AWS CLI with Eucalyptus a plug-in is provided that understands how to access Eucalyptus services.

## Install

To install the Eucalyptus plug-in a Eucalyptus YUM repository must first be enabled, either the release repository:

```bash
yum install https://downloads.eucalyptus.cloud/software/eucalyptus/5/rhel/7/x86_64/eucalyptus-release-5-1.11.as.el7.noarch.rpm
```

or the master repository for the latest nightly build:

```bash
yum install https://downloads.eucalyptus.cloud/software/eucalyptus/master/rhel/7/x86_64/eucalyptus-release-5-1.15.as.el7.noarch.rpm
```

Once a repository is configured, install the plugin and client:

```bash
yum install eucalyptus-awscli-plugin
```

Which will install the plug-in and version 1 of the AWS CLI.

## Configuration

AWS provides general instructions on [Configuring the AWS CLI](https://docs.aws.amazon.com/cli/latest/userguide/cli-chap-configure.html) which includes configuration for credentials. This section covers Eucalyptus plugin specific configuration.

An example configuration for the AWS CLI is:

```bash
# cat .aws/config 
[plugins]
eucalyptus = awscli_plugin_eucalyptus

[default]
ufshost = mycloud.example.com
ufsport = 8773
verify_ssl = yes
output = text
region = eucalyptus
```

The configuration enables the plugin and sets the *ufshost* and *ufsport* to enable Eucalyptus service endpoints to be derived.

If your cloud does not have a valid HTTPS certificate then you will need to change *verify_ssl* to `no`, but note that this is less secure.
