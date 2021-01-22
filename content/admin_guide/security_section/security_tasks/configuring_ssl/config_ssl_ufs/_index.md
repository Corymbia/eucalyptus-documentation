+++
title = "Configure and Enable SSL for the UFS"
weight = 10
+++

This topic details tasks to configure SSL/TLS for the User-Facing Services (UFS)

If you have more than one host (other than node controllers), note the following:

* The keystore must be updated on each host running the eucalyptus-cloud service
* The [key_alias] must be the same on each host
* Use a wildcard certificate (i.e. *.<system.dns.dnsdomain>), since UFS is responsible for all service API endpoints

## Create a Keystore
Eucalyptus uses a PKCS12-format keystore. If you are using a certificate signed by a trusted root CA, perform the following steps. 

Enter the following command to convert your trusted certificate and key into an appropriate format:

    openssl pkcs12 -export -in [YOURCERT.crt] -inkey [YOURKEY.key] \
      -out tmp.p12 -name [key_alias]

{{% notice note %}}
The above command will request an export password, which is used in the following steps.
{{% /notice %}}

Save a backup of the Eucalyptus keystore, at */var/lib/eucalyptus/keys/euca.p12* . Import your keystore into the Eucalyptus keystore on the UFS:

    keytool -importkeystore -srckeystore tmp.p12 -srcstoretype pkcs12 \
      -srcstorepass [export_password] -destkeystore /var/lib/eucalyptus/keys/euca.p12 \
      -deststoretype pkcs12 -deststorepass eucalyptus -alias [key_alias] -destkeypass eucalyptus

## Enable the UFS to Use the Keystore
To enable the UFS to use the keystore, perform the following steps in the CLC because the UFS gets all its configuration information from the CLC. Run the following commands on the CLC: 

    euctl bootstrap.webservices.ssl.server_alias=[key_alias]

## Optional: Redirect Requests to use Port 443
To allow user facing services requests on port 443 instead of the default 8773, run the following commands on the CLC:

    euctl bootstrap.webservices.port=443

