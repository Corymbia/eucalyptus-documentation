+++
title = "Install MidoNet for Eucalyptus"
weight = 5
+++

This topic shows how to install Midokura Enterprise MidoNet for use in your Eucalyptus cloud.
## Install the MidoNet Cluster on the Cloud Controller (CLC)
This topic describes how to install the MidoNet Cluster.MidoNet Cluster services provide a means to manage MidoNet functions that MidoNet agents (Midolman) are unable to perform on their own. MidoNet Cluster services include state synchronization of VxLAN gateways and the MidoNet REST API. A MidoNet v5 deployment requires at least one MidoNet cluster node, and since it replaces the MidoNet API webapp (which was hosted by tomcat in MidoNet v1 series), it must be co-located on the CLC host machine in Eucalyptus deployments. For security reasons, the MidoNet REST API is accessed only on the CLC (localhost interface). 

**To install the MidoNet Cluster on the CLC** 

Add the MidoNet repo file as described in [](install_midokura_prereqs.dita) . Install MidoNet Cluster packages. 
    yum install midonet-cluster python-midonetclient

Edit the */etc/midonet/midonet.conf* file to set the ZooKeeper host IP(s). Replace ZOOKEEPER_HOST_IP in the following example: 
    [zookeeper]
    zookeeper_hosts = ZOOKEEPER_HOST_IP:2181 

Configure cloud-wide access to the NSDB services: 
    cat << EOF | mn-conf set -t default
    zookeeper {
      zookeeper_hosts = “ZOOKEEPER_HOST:2181"
    }
    
    cassandra {
      servers = “CASSANDRA_HOST"
    }
    EOF               

Enable and start the MidoNet Cluster: 
    systemctl enable midonet-cluster.service
    systemctl start midonet-cluster.service

Set the midonet-api end point: 
    mn-conf set cluster.rest_api.http_port=8080
    mn-conf set cluster.rest_api.http_host="127.0.0.1"

Restart the Midonet Cluster so the rest_api parameters take effect: 
    systemctl restart midonet-cluster.service


## Install Midolman on components
This topic describes how to install the Midolman agent.Midolman is the MidoNet Agent, which is a daemon that runs on all hosts where traffic enters and leaves MidoNet. The Midolman agent is required on the Cloud Controller (CLC), Node Controllers (NCs), and any host that is a MidoNet Gateway node (e.g., UFS). **To install Midolman agent** 

Edit the `/etc/midolman/midolman.conf` file to set the ZooKeeper host IP(s). Replace ZOOKEEPER_HOST_IP in the following example: 
    [zookeeper]
    zookeeper_hosts = ZOOKEEPER_HOST_IP:2181

Enable and start Midolman: 
    systemctl enable midolman.service
    systemctl start midolman.service

Configure a Midolman resource usage template. For large Eucalyptus clouds, use the agent-compute-large template. For standard (small or medium) Eucalyptus clouds, use the default template. For gateway nodes, use the agent-gateway templates. 


{{% notice note %}}
For production environments, large templates are recommended. 
{{% /notice %}}


See the [Midolman Installation documentation](http://docs.midokura.com/docs/v5.2/en/quick-start-guide/rhel-7_kilo-rdo/content/_midolman_installation.html) for more information. 

Check MidoNet version # and doc paths each release - match the compat matrix for the release! NOTE that Midokura changes doc repo frequently. GLOBAL SEARCH on "docs.midokura.com" across all docs. Choose the Midolman resource usage template name, based on the size and type of installation: 
    agent-compute-large
    agent-compute-medium
    agent-gateway-large
    agent-gateway-medium
    default

Run this command, replacing `TEMPLATE_NAME` with your chosen template: 
    mn-conf template-set -h local -t TEMPLATE_NAME


## Create a tunnel zone in MidoNet and add hosts
This topic describes how to create a MidoNet tunnel zone.In MidoNet, a tunnel zone is an isolation zone for hosts. Physical hosts that are members of a given tunnel zone communicate directly with one another and establish network tunnels as needed, and on demand. These network tunnels are used to transport overlay traffic (e.g., inter-VM communication) and isolate the underlay physical network communication (i.e., inter-physical hosts communication). On a Eucalyptus deployment, one MidoNet tunnel zone is expected with the IP address on the physical network designated to carry VM traffic being used when configuring its members. Eucalyptus accepts the following tunnel zone names: 

* eucatz 
* euca-tz 
* midotz 
* mido-tz 
For more information, see [What are Tunnel Zones?](http://docs.midokura.com/docs/v5.2/en/operations-guide/content/tunnel_zones.html) 

Note to WRITER: Yep, it's "underlay physical network" https://docs.midonet.org/docs/v5.2/en/reference-architecture/content/underlay_network.html (not "underlying physical network") **To create a tunnel zone in MidoNet** 

Log into the MidoNet shell. For example: 
    midonet-cli -A --midonet-url=http://127.0.0.1:8080/midonet-api

Create a GRE tunnel zone: 
    [root@clcfrontend mido-docs]# midonet-cli -A --midonet-url=http://127.0.0.1:8080/midonet-api
    midonet> tunnel-zone add name eucatz type gre
    midonet> tunnel-zone list
    tzone tzone0 name eucatz type gre
    midonet> host list
    host host0 name node1 alive true
    host host1 name clcfrontend alive true
    host host2 name node2 alive true

You should see a host listed for each of your Node Controllers and for your User Facing Service host; if not, check the `/var/log/midolman/midolman.log` log file on the missing hosts to ensure there are no error messages. 

After verifying all your hosts are listed, add each host to your tunnel zone as follows. Replace HOST_N_IP with the IP of your Node Controller or User Facing Service host that you used to register the component with Eucalyptus : 
    midonet> tunnel-zone tzone0 add member host host0 address HOST_0_IP
    midonet> tunnel-zone tzone0 add member host host1 address HOST_1_IP
    midonet> tunnel-zone tzone0 add member host host2 address HOST_2_IP

You are now ready to install and configure Eucalyptus to use this MidoNet installation. 
## Additional ZooKeeper Configuration
Ongoing data directory cleanup is required for ZooKeeper.This should be moved to the Admin Guide when networking docs are rearranged further. The following parameters should be added in */etc/zookeeper/zoo.cfg* for automatic purging of the snapshots and corresponding transaction logs: 
    autopurge.snapRetainCount=3  # The number of snapshots to retain in dataDir
    autopurge.purgeInterval=1  # Purge task interval in hours

Check ZooKeeper version # and doc paths each release - match the compat matrix for the release! For more information, see [ZooKeeper Admin Guide, Ongoing Data Directory Cleanup](http://zookeeper.apache.org/doc/r3.4.8/zookeeperAdmin.html#Ongoing+Data+Directory+Cleanup) . 

