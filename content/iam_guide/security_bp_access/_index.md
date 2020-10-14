+++
title = "Authentication and Access Control Best Practices"
weight = 40
+++

This topic describes best practices for Identity and Access Management and the account.
## Identity and Access Management
Eucalyptus manages access control through an authentication, authorization, and accounting system. This system manages user identities, enforces access controls over resources, and provides reporting on resource usage as a basis for auditing and managing cloud activities. The user identity organizational model and the scheme of authorizations used to access resources are based on and compatible with the AWS Identity and Access Management (IAM) system, with some Eucalyptus extensions provided that support ease-of-use in a private cloud environment. 

For a general introduction to IAM in Eucalyptus, see [Access Concepts]({{< ref concepts_eiam.md >}}) in the IAM Guide. For information about using IAM quotas to enforce limits on resource usage by users and accounts in Eucalyptus, see the [Quotas]({{< ref access_policy_quota.md >}}) section in the IAM Guide. 

The [Amazon Web Services IAM Best Practices](http://docs.aws.amazon.com/IAM/latest/UserGuide/IAMBestPractices.html) are also generally applicable to Eucalyptus. 


## Credential Management
Protection and careful management of user credentials (passwords, access keys, X.509 certificates, and key pairs) is critical to cloud security. When dealing with credentials, we recommend: 



* Limit the number of active credentials and do not create more credentials than needed. 
* Only create users and credentials for the interfaces that you will actually use. For example, if a user is only going to use the Management Console, do not create credentials access keys for that user. 
* Use and or to get a specific set of credentials if needed. 
* Regularly check for active credentials using commands and remove unused credentials. Ideally, only one pair of active credentials should be available at any time. 
* Rotate credentials regularly and delete old credentials as soon as possible. Credentials can be created and deleted using commands, such as and . 
* When rotating credentials, there is an option to deactivate, instead of removing, existing access/secret keys and X.509 certificates. Requests made using deactivated credentials will not be accepted, but the credentials remain in the Eucalyptus database and can be restored if needed. You can deactivate credentials using and . 

## Privileged Roles
The `eucalyptus` account is a super-privileged account in Eucalyptus. It has access to all cloud resources, cloud setup, and management. The users within this account do not obey IAM policies and compromised credentials can result in a complete cloud compromisation that is not easy to contain. We recommend limiting the use of this account and associated users' credentials as much as possible. 

For all unprivileged operations, use regular accounts. If you require super-privileged access (for example, management of resources across accounts and cloud setup administration), we recommend that you use one of the predefined privileged roles. 

The Account, Infrastructure, and Resource Administrator [roles]({{< ref access_roles.md >}}) provide a more secure way to gain super privileges in the cloud. Credentials returned by an assume-role operation are short-lived (unlike regular user credentials). Privileges available to each role are limited in scope and can be revoked easily by modifying the trust or access policy for the role. 

