+++
title = "LDAP Security"
weight = 5
+++

This topic explains variables in the LIC file you should use to secure configuration.When you enable LDAP/Active Directory (AD) integration with Eucalyptus, we recommend that you use the following variables in the LDAP/AD Integration Configuration (LIC) file. These variables are located under the `ldap-service` element in the LIC file. 


| Element | Description | 
|  :---- |  :---- | 
| auth-method | The LDAP/AD authentication method to perform synchronization. Supports three types of methods: simple: for clear text user/password authentication.DIGEST-MD5: for SASL authentication using MD5GSSAPI: SASL authentication using Kerberos V5. | 
| user-auth-method | The LDAP/AD authentication method for normal users to perform Management Console login. Supports three types of methods:simple: for clear text user/password authentication.DIGEST-MD5: for SASL authentication using MD5GSSAPI: SASL authentication using Kerberos V5. | 
| use-ssl | Specifies whether to use SSL for connecting to LDAP/AD service. If this option is enabled, make sure the SSL port for LDAP is defined as part of the server-url. The default port for LDAP+SSL is port 636. | 
| ignore-ssl-cert-validation | Specifies whether to ignore self-signed SSL certs. This is useful when you only have self-signed SSL certs for your LDAP/AD services. | 
| krb5-conf | The file path for krb5.conf, if you use GSSAPI authentication method. | 

When use-ssl is enabled, ldaps will be used. However, the `server-url` still needs to begin with `ldap://` . 

We recommend using a proxy user for the `auth-principal` . Typically, proxy users are used to associate with the application that needs to do reads (and in some cases writes) against the LDAP/AD directory. Proxy users also make it easier for security audits done on the LDAP/AD directory. To use with Eucalyptus and the LDAP/AD sync, the proxy user only needs read access. For more information about using proxy authentication with OpenLDAP and Active Directory, go to the following resources: 



* For LDAP: (see the section) 
* For Active Directory: 
* 
For more information about LDAP and security, go to the following resources: 



* (see the section) 
* 
* 
For more information about Active Directory and security, go to the following resources: 



* 
* 
* 
