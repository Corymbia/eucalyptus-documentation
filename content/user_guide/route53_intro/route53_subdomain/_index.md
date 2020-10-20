+++
title = "Route53 Delegated Subdomain"
weight = 30
+++

When using Route53 the Hosted Zone is often a subdomain for a domain managed using external DNS. In this case the external DNS must be updated to delegate management of the subdomain to your
hosted zones name servers.

## Hosted Zone Name Servers
When you create a public Hosted Zone in Eucalyptus it will be allocated some nameservers. You can use the AWS CLI to determine the Name Servers for your zone:

```bash
# aws route53 list-hosted-zones
HOSTEDZONES	87a20e2b-f835-4775-a6ad-16f14033668a	/hostedzone/ZAAKJGJPMUHV32	subdomain.example.com.	2
CONFIG	False
#
# aws route53 list-resource-record-sets --hosted-zone-id ZAAKJGJPMUHV32 --query "ResourceRecordSets[?Type == 'NS']"
subdomain.example.com.	900	NS
RESOURCERECORDS	ns1.mycloud.example.com.
```

To discover the nameservers, first list the hosted zone to find the identifer and then pass the identifer to *list-resource-record-sets*. The example above uses a query to output only the *NS* information.

## External Name Server records
The external DNS should be updated to add a Name Server *NS* record and a corresponding *A* record to map that name to an IP address:

```
subdomain.example.com	    NS	ns1.mycloud.example.com.
ns1.mycloud.example.com	A	1.X.Y.123
```

{{% notice note %}}
The external DNS must not have an SOA record for the delegated subdomain as your Hosted Zone in Eucalyptus Route53 is authoritative.
{{% /notice %}}
