+++
title = "Automated Eucalyptus Installation"
weight = 25
+++


Automated Eucalytpus installation uses an [Ansible](https://www.ansible.com/overview/how-ansible-works) playbook.

{{% notice note %}}
Before starting the automated installation CentOS or RHEL 7.9 should be installed on all hosts.
{{% /notice %}}

To install Eucalyptus you will need to have Ansible and the Eucalyptus playbooks available and to create an *inventory* file that describes your deployment.

## Install Packages

The host performing the installation must have the EPEL YUM repository available (for Ansible):

```bash
yum install epel-release
```

and a Eucalyptus YUM repository, either the snapshot repository:

```bash
yum install http://downloads.eucalyptus.cloud/software/eucalyptus/snapshot/5/rhel/7/x86_64/eucalyptus-release-5-1.10.as.el7.noarch.rpm
```

or the master repository for the latest nightly build:

```bash
yum install http://downloads.eucalyptus.cloud/software/eucalyptus/master/rhel/7/x86_64/eucalyptus-release-5-1.15.as.el7.noarch.rpm
```

{{% notice note %}}
These are pre-releases for Eucalytpus 5. Once Eucalyptus 5 is released the release repository will be available and should be preferred.
{{% /notice %}}

## Create Inventory

The Ansible inventory file describes both the hosts that will run your Eucalyptus cloud and the options for your installation.

```yaml
---
all:
  hosts:
    cloud.example.com:
    node[01:10].example.com:

  vars:
    vpcmido_public_ip_range: "1.X.Y.128-1.X.Y.254"
    vpcmido_public_ip_cidr: "1.X.Y.128/25"

  children:
    cloud:
      hosts:
        cloud.example.com:
    zone:
      hosts:
        cloud.example.com:
    nodes:
      hosts:
        node[01:10].example.com:

```

There are three main sections to an inventory file:

1. *hosts* : the hosts to deploy
1. *vars* : variables providing options for the deployment
1. *children* : host groupings that describe where to install Eucalyptus components

### Minimal Install

The minimum inventory for a deployment must specify one host and have a *children*/*cloud* section that includes that host.

For `VPCMIDO` the *vars* for *vpcmido_public_ip_range* and *vpcmido_public_ip_cidr* must also be provided.

When the *zone* and *nodes* children are not specified they are assumed to be the same host as the *cloud*.

### Customization

Settings that are often used in an inventory are described in this section.

The DNS domain to be used should be set in the *vars* section:

```yaml
    cloud_system_dns_dnsdomain: "mycloud.example.com"
```

The NTP server to use with services in your deployment can also be specifed:

```yaml
    cloud_properties:
      services.imaging.worker.ntp_server: "time.cloudflare.com"
      services.loadbalancing.worker.ntp_server: "time.cloudflare.com"
```

{{% notice note %}}
The *cloud_properties* section allows you configure any settings that you would later set using *euctl*
{{% /notice %}}

To specify region and zone names for your deployment add the *vars*:

```yaml
    cloud_region_name: "us-euca-1"
    cloud_zone_1_name: "us-euca-1a"
    cloud_zone_2_name: "us-euca-1b"
    cloud_zone_3_name: "us-euca-1c"
```

You can follow AWS naming conventions or can use your own naming scheme. To specify which hosts belong to which zone update the `hosts` section:

```yaml
  hosts:
    node01.example.com:
      host_cluster_ipv4: "10.111.10.101"
      host_public_ipv4: "1.X.Y.101"
      host_zone_key: 1
```

The *host_zone_key* value of `1` specifes that `node01` would be part of the `us-euca-1a` zone. This example also shows how to configure the public and cluster IP addresses for a host.

To specify the port for web sevices use:

```yaml
    cloud_public_port: 443
```

If using port `443` for web services, the management console should be deployed as a service to avoid a port conflict.

To enable a firewall on the public/cluster interfaces use:

```yaml
    cloud_firewalld_configure: yes
    cloud_firewalld_cluster_cidr: "10.111.0.0/16"
    cloud_firewalld_cluster_interface: "en2"
    cloud_firewalld_public_interface: "en1"
```

Interfaces must be named consistently on all hosts.

The default install uses *overlay* for block storage, to use *das* you must have an LVM volume group available on all storage (*zone*) hosts and set:

```yaml
    cloud_storage_dasdevice: "storage_vg"
```

To deploy the management console as service running on an instance in your Eucalyptus cloud:

```yaml
    eucalyptus_console_cloud_deploy: yes
    cloud_service_image_rpm: no
```

This will also create a DNS entry for the console such as `console.mycloud.example.com`. When deploying the console on an instance it is recommended to also set *cloud_service_image_rpm* to `no` so that the service image for loadbalancing and imaging is installed using the same approach rather than from the rpm.

### MidoNet NSDB

For `VPCMIDO` deployments the MidoNet NSDB (Network State Database) should be deployed on multiple hosts:

```yaml
    midonet-nsdb:
      hosts:
        midonet-nsdb[01:03].example.com:
```

These could be distinct hosts, or could be hosts running cloud and zone components (for example)

### Using Ceph

To use Ceph for block and object storage configure the settings:

```yaml
    ceph_release: "nautilus"
    ceph_osd_data_path: "storage_vg/storage_lv"
    ceph_public_network: "10.111.0.0/16"
```

the *ceph_osd_data_path* should reference either an existing LVM volume available on all hosts or a device.

The hosts for ceph must be in the *ceph* group under *children*:

```yaml
    ceph:
      hosts:
        ceph[01:03].example.com:
```

There must be three or more hosts to have redundancy.

### Using MinIO

To deploy MinIO as the objectstorage provider you specify *minio* under *children*:

```
    minio:
      hosts:
        minio.example.com:

```

This will deploy MinIO on those hosts and also configure MinIO as the objectstorage provider when Ceph is not being deployed. There must be three or more hosts to have redundancy.

### Enabling Certbot Integration

To enable [Let's Encrypt](https://letsencrypt.org) for HTTPS via certbot set the following *vars*:

```
    eucaconsole_certbot_configure: yes
    eucalyptus_console_certbot_enable: yes
    eucalyptus_services_certbot_enable: yes
```

To use this functionality the cloud must be public so that it can be reached for DNS (services) or HTTP (console) challenges. See the Let's Encrypt [Challenge Types](https://letsencrypt.org/docs/challenge-types/) for details.

The *eucaconsole_certbot_configure* setting should be used when deploying the console on a physical host. The *eucalyptus_console_certbot_enable* setting applies when deploying the console on the cloud (i.e. when you specifed *eucalyptus_console_cloud_deploy*)

## Test Connectivity

Before starting a deployment, test that the installation host can access all hosts in the inventory by running:

```bash
ansible --inventory inventory.yml -m ping all
```

If this fails, ensure that you have configured SSH access to all inventory hosts (e.g. configure passwordless SSH access) before proceeding to the installation.

## Perform Installation

To start a `VPCMIDO` installation:

```bash
ansible-playbook --inventory inventory.yml /usr/share/eucalyptus-ansible/playbook_vpcmido.yml
```

To start an `EDGE` installation:

```bash
ansible-playbook --inventory inventory.yml /usr/share/eucalyptus-ansible/playbook_edge.yml
```

See the [Find More Information]({{< ref what_next >}}) page for next steps.

