+++
title = "Configure and Enable SSL for the UFS"
weight = 10
+++

This topic details tasks to configure SSL for the User-Facing Services (UFS).
{{% notice note %}}
If you have multiple USF machines, note the following: 
{{% /notice %}}

## Create a Keystore
Eucalyptus uses a PKCS12-format keystore. If you are using a certificate signed by a trusted root CA, perform the following steps. 

Enter the following command to convert your trusted certificate and key into an appropriate format: 
    openssl pkcs12 -export -in [YOURCERT.crt] -inkey [YOURKEY.key] \
     -out tmp.p12 -name [key_alias]

This command will request an export password, which is used in the following steps. Save a backup of the Eucalyptus keystore, at */var/lib/eucalyptus/keys/euca.p12* . Import your keystore into the Eucalyptus keystore on the UFS: 
    keytool -importkeystore -srckeystore tmp.p12 -srcstoretype pkcs12 
    -srcstorepass [export_password] -destkeystore /var/lib/eucalyptus/keys/euca.p12 
    -deststoretype pkcs12 -deststorepass eucalyptus -alias [key_alias] -destkeypass eucalyptus


## Enable the UFS to Use the Keystore
To enable the UFS to use the keystore, perform the following steps in the CLC because the UFS gets all its configuration information from the CLC. Run the following commands on the CLC: 
    euctl bootstrap.webservices.ssl.server_alias=[key_alias]
    euctl bootstrap.webservices.ssl.server_password=[export_password]


## Optional: Redirect Requests to use Port 443
To direct all user facing services requests to use port 443 instead of using 8773, run the following commands on the CLC: 


    euctl bootstrap.webservices.port=443
    euctl bootstrap.webservices.default_ec2_uri_scheme=https
    euctl bootstrap.webservices.default_euare_uri_scheme=https
    euctl bootstrap.webservices.default_s3_uri_scheme=https


## Enable SSL
To enable SSL, both the UFS and CLC must be restarted. Restart the UFS and CLC by running service eucalyptus-cloud restart or 


    /etc/init.d/eucalyptus-cloud restart

