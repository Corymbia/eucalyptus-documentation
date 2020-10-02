+++
title = "Adding SSL Support"
weight = 5
+++

This topic describes how to add SSL support to a new or existing load balancer.
## Creating a new listener with SSL support
This task shows how to create a new listener with SSL support.
{{% notice note %}}
In order to use HTTPS support, you'll need to install an SSL server certificate on your load balancer. If you haven't already done this, see . 
{{% /notice %}}
To add a new listener to your load balancer: Using the ARN for the certificate you installed, use the `eulb-create-listener` command to create a new listener. For example: `eulb-create-lb-listeners MyLoadBalancer --listener "protocol=HTTPS,lb-port=443,instance-port=80,instance-protocol=HTTP, cert-id=arn:aws:iam::12345678901:my-server-certificate/testing/myNewCert"` Use the `eulb-describe-lbs` command to see the details of your load balancer. For example: `eulb-describe-lbs MyLoadBalancer` 
## Updating a listener with a new SSL certificate
This task shows how to replace an SSL server certificate configured with listeners"
{{% notice note %}}
In order to use HTTPS support, you'll need to install an SSL server certificate on your load balancer. If you haven't already done this, see . 
{{% /notice %}}
To update an existing listener with SSL support: Use the `eulb-set-lb-listener-ssl-certcommand` with the ARN of your new server certificate to replace the certificate configured with listeners For example: `eulb-set-lb-listener-ssl-cert MyLoadBalancer --lb-port 443 --cert-id arn:aws:iam::12345678901:my-server-certificate/testing/myNewCert` Use the `eulb-describe-lbs` command to see the details of your load balancer. For example: `eulb-describe-lbs MyLoadBalancer` 