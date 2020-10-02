+++
title = "ldap-service"
weight = 10
+++

The element contains everything related to the LDAP/AD service.

| Element | Description | 
|  :---- |  :---- | 
| server-url | The LDAP/AD server URL, starting with ldap://. | 
| auth-method | The LDAP/AD authentication method to perform synchronization. | 
| auth-principal | The ID of the administrative user for synchronization. | 
| auth-credentials | The credentials for LDAP/AD authentication, like a password. We recommend that you encrypt this using /usr/sbin/euca-lictool. | 
| user-auth-method | The LDAP/AD authentication method for normal users to perform Management Console login. simple: for clear text user/password authentication.DIGEST-MD5: for SASL authentication using MD5GSSAPI: SASL authentication using Kerberos V5. | 
| use-ssl | Specifies whether to use SSL for connecting to LDAP/AD service. If this option is enabled, make sure the SSL port for LDAP is defined as part of the server-url. The default port for LDAP+SSL is port 636. | 
| ignore-ssl-cert-validation | Specifies whether to ignore self-signed SSL certs. This is useful when you only have self-signed SSL certs for your LDAP/AD services. | 
| krb5-conf | The file path for krb5.conf, if you use GSSAPI authentication method. | 

