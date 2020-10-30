+++
title = "Route53 Concepts"
weight = 10
+++

This section describes the important concepts for the Route53 service and for Domain Name System (DNS)

### Public and Private Hosted Zones
A public hosted zone describes how to route traffic for a public domain, such as **example.com**, and its subdomains. Information in a public hosted zone is available to anyone that can connect to your Eucalyptus deployment.

A private hosted zone describes how to route traffic for a domain and its subdomains within a VPC managed using Eucalyptus EC2 VPC service. Private zones are useful for repeatable deployments using well-known names.

### Resource Record Sets
After you create a hosted zone for your domain, such as **example.com**, you create resource record sets to tell the Domain Name System (DNS) how to route traffic for that domain.

For example you would create an **A** record to map the name **resource.example.com** to the public IP address of an EC2 instance.

## DNS Concepts
Important concepts related to underlying DNS functionality are:

* **Alias** : An alias connects a name to a cloud resource such as an Elastic Load Balancer
* **CName** : A *CNAME* resource record redirects to another name. *CNAMES* are often used with S3 buckets.
* **IP Address** : An *A* resource record maps a name to an IP address used to access a resource such as an EC2 instance.
* **TTL** : The Time To Live (TTL) of a resource record is important for controlling how long clients can cache DNS information.

