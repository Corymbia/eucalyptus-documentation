+++
title = "Configure SSL"
weight = 20
+++

In order to connect to Eucalyptus using SSL/TLS, you must have a valid certificate for the Cloud Controller (CLC)

If you have more than one host (other than node controllers), note the following:

* The keystore must be updated on each host running the eucalyptus-cloud service
* The [key_alias] must be the same on each host
* Use a wildcard certificate (i.e. *.<system.dns.dnsdomain>), since UFS is responsible for all service API endpoints


## Create a keystore
Eucalyptus uses a PKCS12-format keystore. If you are using a certificate signed by a trusted root CA, use the following command to convert your trusted certificate and key into an appropriate format:

    openssl pkcs12 -export -in [YOURCERT.crt] -inkey [YOURKEY.key] \
      -out tmp.p12 -name [key_alias]

{{% notice note %}}
The above command will request an export password, which is used in the following steps.
{{% /notice %}}

Save a backup of the Eucalyptus keystore, at */var/lib/eucalyptus/keys/euca.p12* , and then import your keystore into the Eucalyptus keystore as follows:

    keytool -importkeystore \
      -srckeystore tmp.p12 -srcstoretype pkcs12 -srcstorepass [export_password] \
      -destkeystore /var/lib/eucalyptus/keys/euca.p12 -deststoretype pkcs12 \
      -deststorepass eucalyptus -alias [key_alias] \
      -srckeypass [export_password]

## Enable the Cloud Controller to use this keystore
Run the following commands on the Cloud Controller (CLC): 

    euctl bootstrap.webservices.ssl.server_alias=[key_alias]

## Optional: Redirect Requests to use Port 443
To allow user facing services requests on port 443 instead of the default 8773, run the following commands on the CLC:

    euctl bootstrap.webservices.port=443


