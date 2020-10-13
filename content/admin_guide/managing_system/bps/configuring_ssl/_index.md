+++
title = "Configure SSL"
weight = 20
+++

In order to connect to Eucalyptus using SSL, you must have a valid certificate for the Cloud Controller (CLC). You must also be running the Cloud Controller and Cluster Controller (CC) on separate machines.
## Create a keystore
Eucalyptus uses a PKCS12-format keystore. If you are using a certificate signed by a trusted root CA, use the following command to convert your trusted certificate and key into an appropriate format: 



    openssl pkcs12 -export -in [YOURCERT.crt] -inkey [YOURKEY.key] \
     -out tmp.p12 -name [key_alias]

**Note** : this command will request an export password, which is used in the following steps. 

Save a backup of the Eucalyptus keystore, at */var/lib/eucalyptus/keys/euca.p12* , and then import your keystore into the Eucalyptus keystore as follows: 



    keytool -importkeystore \ 
    -srckeystore tmp.p12 -srcstoretype pkcs12 -srcstorepass [export_password] \ 
    -destkeystore /var/lib/eucalyptus/keys/euca.p12 -deststoretype pkcs12 \ 
    -deststorepass eucalyptus -alias [key_alias] \ 
    -srckeypass [export_password] 


## Enable the Cloud Controller to use this keystore
Run the following commands on the Cloud Controller (CLC): 



    euctl bootstrap.webservices.ssl.server_alias=[key_alias]
    euctl \ bootstrap.webservices.ssl.server_password=[export_password]

Restart the CLC by running `systemctl restart eucalyptus-cloud.service` or `systemctl restart eucalyptus-cloud.service` . 


## Optional: Configure the Cloud Controller to redirect requests on port 443 to port 8773
The Cloud Controller listens for both SSL and non-SSL connections on port 8773. If you have other tools that expect to speak SSL on port 443, you should forward requests on that port to port 8773. For example, the following iptables command can be used: 



    iptables -t nat -A PREROUTING -p tcp --dport 443 -j REDIRECT --to-ports 8773

