+++
title = "Uploading SSL Certificates for Elastic Load Balancing"
weight = 5
+++

..  _elb_examples_basic_config:

You must install an X.509 certificate on your load balancer in order to use HTTPS or SSL termination. The X.509 certificate is issued by a central Certificate Authority (CA) and contains identifying information, including a digital signature. X.509 certificates have a validity period. Once an X.509 certificate expires, you must create and install a new certificate.

=====================
Upload a Certificate
=====================

Once you've created a certificate, you must upload it to your cloud using the command.{{% notice note %}}You must create the certificate and get it signed by a certificate authority (CA) before you can upload the certificate using the AWS Identity and Access Management (IAM) service. For instructions, go to . {{% /notice %}}To upload a certificate : 

Enter the ``euare-servercertupload`` command, specifying the name of your certificate, the contents of the PEM-encoded public- and private-keys: 

.. code::

  euare-servercertupload -s cert-name --certificate-file ssl_server_cert.crt --private-key-file ssl_server_cert.pem

You've now created an elastic load balancer. 

=========================
Verify Server Certificate
=========================

You can verify that an uploaded certificate is stored in IAM. Each certificate object has a unique Amazon Resource Name (ARN) and ID.To verify an uploaded certificate: Use the ``euare-servercertlistbypath`` command to verify the certificate is stored in IAM: 

.. code::

  euare-servercertgetattributes -s elb-ssl-cert

The command will return the ARN, followed by the GUID. For example: 



.. code::

  arn:aws:iam::495375389014:server-certificate/elb-ssl-cert
  ASCWDKTJBXPSZTHWFERVP

