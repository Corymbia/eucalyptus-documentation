+++
title = "Configure Eucalyptus DNS"
weight = 10
+++

Eucalyptus provides a DNS service that maps service names, bucket names, and more to IP addresses. This section details how to configure the Eucalyptus DNS service.
{{% notice note %}}
administration tools are designed to work with DNS-enabled clouds, so configuring this service is highly recommended. The remainder of this guide is written with the assumption that your cloud is DNS-enabled. 
{{% /notice %}}
The DNS service will automatically try to bind to port 53. If port 53 cannot be used, DNS will be disabled. Typically, other system services like dnsmasq are configured to run on port 53. To use the Eucalyptus DNS service, you must disable these services. 


## Configure the Domain and Subdomain
Before using the DNS service, configure the DNS subdomain name that you want Eucalyptus to handle using the steps that follow. 

Log in to the CLC and enter the following: 
    euctl system.dns.dnsdomain=mycloud.example.com

You can configure the load balancer DNS subdomain. To do so, log in to the CLC and enter the following: 
    euctl services.loadbalancing.dns_subdomain=lb


## Turn on IP Mapping
To enable mapping of instance IPs to DNS host names: 

Enter the following command on the CLC: 
    euctl bootstrap.webservices.use_instance_dns=true

When this option is enabled, public and private DNS entries are created for each launched instance in Eucalyptus . This also enables virtual hosting for Walrus. Buckets created in Walrus can be accessed as hosts. For example, the bucket `mybucket` is accessible as `mybucket.objectstorage.mycloud.example.com` . 

Instance IP addresses will be mapped as `euca-A-B-C-D.eucalyptus.mycloud.example.com` , where `A-B-C-D` is the IP address (or addresses) assigned to your instance. 

If you want to modify the subdomain that is reported as part of the instance DNS name, enter the following command: 
    euctl cloud.vmstate.instance_subdomain=.custom-dns-subdomain

When this value is modified, the public and private DNS names reported for each instance will contain the specified custom DNS subdomain name, instead of the default value, which is `eucalyptus` . For example, if this value is set to `foobar` , the instance DNS names will appear as `euca-A-B-C-D.foobar.mycloud.example.com` . 


{{% notice note %}}
The code example above correctly begins with "." before . 
{{% /notice %}}

## Enable DNS Delegation
DNS delegation allows you to forward DNS traffic for the Eucalyptus subdomain to the Eucalyptus CLC host. This host acts as a name server. This allows interruption-free access to Eucalyptus cloud services in the event of a failure. The CLC host is capable of mapping cloud host names to IP addresses of the CLC and UFS / OSG host machines. 

For example, if the IP address of the CLC is `192.0.2.5` , and the IP address of Walrus is `192.0.2.6` , the host `compute.mycloud.example.com` resolves to `192.0.2.5` and `objectstorage.mycloud.example.com` resolves to `192.0.2.6` . 

To enable DNS delegation: 

Enter the following command on the CLC: 
    euctl bootstrap.webservices.use_dns_delegation=true


## Configure the Master DNS Server
Set up your master DNS server to delegate the Eucalyptus subdomain to the UFS host machines, which act as name servers. 

The following example shows how the Linux name server `bind` is set up to delegate the Eucalyptus subdomain. 

Open */etc/named.conf* and set up the `example.com` zone. For example, your */etc/named.conf* may look like the following: 
    zone "example.com" IN {
    	      type master;
    	      file "/etc/bind/db.example.com";
    	      };
    	    

Create */etc/bind/db.example.com* if it does not exist. If your master DNS is already set up for `example.com` , you will need to add a name server entry for UFS host machines. For example: 
    $ORIGIN example.com.
    $TTL 604800
    
    @ IN    SOA ns1 admin.example.com 1 604800 86400 2419200 604800
            NS  ns1
    ns1     A   MASTER.DNS.SERVER_IP
    ufs1    A   UFS1_IP
    mycloud NS  ufs1

After this, you will be able to resolve your instances' public DNS names such as `euca-A-B-C-D.eucalyptus.mycloud.example.com` . 

Restart the bind nameserver `service named restart` . Verify your setup by pointing */etc/resolv.conf* on your client to your primary DNS server and attempt to resolve `compute.example.com` using ping or nslookup. It should return the IP address of a UFS host machine. 
## Advanced DNS Options
Recursive lookups and split-horizon DNS are available in Eucalyptus . 

To enable any of the DNS resolvers, set `dns.enabled` to `true` . To enable the recursive DNS resolver, set `dns.recursive.enabled` to `true` . To enable split-horizon DNS resolution for internal instance public DNS name queries, set `dns.split_horizon.enabled` to `true` . 
## Optional: Configure Eucalyptus DNS to Spoof AWS Endpoints
You can configure instances to use AWS region FQDNs for service endpoints by enabling DNS spoofing. 

Set up a Eucalyptus cloud with Eucalyptus DNS and HTTPS endpoints. When creating CSR, make sure and add Subject Alternative Names for all the supported AWS services for the given region that’s being tested. For example: 
    $ openssl req -in wildcard.c-06.autoqa.qa1.eucalyptus-systems.com.csr 
    						-noout -text | less X509v3 Subject Alternative Name:
         DNS:ec2.us-east-1.amazonaws.com, DNS:autoscaling.us-east-1.amazonaws.com, 
         DNS:cloudformation.us-east-1.amazonaws.com, DNS:monitoring.us-east-1.amazonaws.com, 
         DNS:elasticloadbalancing.us-east-1.amazonaws.com, DNS:s3.amazonaws.com, 
         DNS:sts.us-east-1.amazonaws.com

Set DNS spoofing: 
    [root@d-17 ~]#  euctl dns.spoof_regions --region euca-admin@future
    dns.spoof_regions.enabled = true
    dns.spoof_regions.region_name =
    dns.spoof_regions.spoof_aws_default_regions = true
    dns.spoof_regions.spoof_aws_regions = true

Launch an instance, and allow SSH access. SSH into the instance and install AWS CLI. 
    ubuntu@euca-172-31-12-59:~$ sudo apt-get install -y python-pip
    ubuntu@euca-172-31-12-59:~$ sudo -H pip install --upgrade pip
    ubuntu@euca-172-31-12-59:~$ sudo -H pip install --upgrade awscli

Run `aws configure` and set access and secret key information if not using instance profile. Confirm AWS CLI works with HTTPS Eucalyptus service endpoint: 
    ubuntu@euca-172-31-12-59:~$ aws --ca-bundle euca-ca-0.crt 
    --endpoint-url https://ec2.c-06.autoqa.qa1.eucalyptus-systems.com/ ec2 describe-key-pairs
    {
        "KeyPairs": [
            {
                "KeyName": "devops-admin",
                "KeyFingerprint": "ee:4f:93:a8:87:8d:80:8d:2c:d6:d5:60:20:a3:2d:b2"
            }
        ]
    }

Test against AWS FQDN service endpoint that matches one of the SANs in the signed certificate: 
    ubuntu@euca-172-31-12-59:~$ aws --ca-bundle euca-ca-0.crt 
    --endpoint-url https://ec2.us-east-1.amazonaws.com ec2 describe-key-pairs{
        "KeyPairs": [
            {
                "KeyName": "devops-admin",
                "KeyFingerprint": "ee:4f:93:a8:87:8d:80:8d:2c:d6:d5:60:20:a3:2d:b2"
            }
        ]
    }				

