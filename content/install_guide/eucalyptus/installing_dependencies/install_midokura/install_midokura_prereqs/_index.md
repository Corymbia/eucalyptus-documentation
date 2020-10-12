+++
title = "Prerequisites"
weight = 10
+++

This topic discusses the prerequisites for installing MidoNet 5.2.

You need to configure software repositories and install Network State Database (NSDB) services: ZooKeeper and Cassandra. 

## Repository Access
In order to use MidoNet with Eucalyptus you need to configure the MidoNet repositories.

Create `/etc/yum.repos.d/midonet.repo` and `/etc/yum.repos.d/midonet-misc.repo` on all host machines that will run MidoNet components including ZooKeeper and Cassandra. For example: 

    [midonet]
    name=MidoNet
    baseurl=http://builds.midonet.org/midonet-5.2/stable/el7/
    enabled=1
    gpgcheck=1
    gpgkey=https://builds.midonet.org/midorepo.key

and:

    [midonet-misc]
    name=MidoNet 3rd Party Tools and Libraries
    baseurl=http://builds.midonet.org/misc/stable/el7/
    enabled=1
    gpgcheck=1
    gpgkey=https://builds.midonet.org/midorepo.key

See [MidoNet Repository Configuration](https://docs.midonet.org/docs/latest-en/quick-start-guide/rhel-7_newton-rdo/content/_repository_configuration.html). 

## ZooKeeper
MidoNet uses Apache ZooKeeper to store critical path data about the virtual and physical network topology. 

For a simple single-server installation, install ZooKeeper on any server that is IP accessible from all Midolman agents (for example: on the CLC host machine itself). You can also cluster ZooKeeper for fault tolerance. See [MidoNet NSDB ZooKeeper Installation](https://docs.midonet.org/docs/latest-en/quick-start-guide/rhel-7_newton-rdo/content/_zookeeper_installation.html).

Enable and start the ZooKeeper service before installing the other MidoNet services. 


## Cassandra
MidoNet uses Apache Cassandra to store flow state information. 

For a simple single-server installation, install Cassandra on any server that is IP accessible from all Midolman agents (for example: on the CLC host machine itself). You can also cluster Cassandra for fault tolerance. See [MidoNet NSDB Cassandra Installation](https://docs.midonet.org/docs/latest-en/quick-start-guide/rhel-7_newton-rdo/content/_cassandra_installation.html).

Enable and start the Cassandra service before installing the other MidoNet services. 

