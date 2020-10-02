+++
title = "Verify the Services"
weight = 10
+++

This topic describes how to verify all the services after upgrading.Verify that all Eucalyptus components are running and properly connected to one another. Check to make sure that the status of each service is enabled. 

To verify that all services are enabled: 

Verify the Eucalyptus versions. For example: 
    # euca-version
    euca2ools 
    eucalyptus 

If you are using the Walrus backend for object storage, verify your Walrus backend service: 
    euserv-describe-services --filter service-type=walrusbackend

Eucalyptus returns a result, as in the following example. 


    SERVICE walrusbackend walrus enabled

Verify your CCs: 
    euserv-describe-services --filter service-type=cluster

Eucalyptus returns a list, as in the following example. 


    SERVICE cluster one one-cc enabled
    SERVICE cluster two two-cc enabled

Verify your SCs: 
    euserv-describe-services --filter service-type=storage

Eucalyptus returns a list, as in the following example. 


    SERVICE storage one one-sc enabled
    SERVICE storage one one-sc enabled

Make sure that NCs are presenting available resources to the CC. 
    euca-describe-instance-types --show-capacity --by-zone

The returned output should a non-zero number in the `Total` column, as in the following example. 


    AVAILABILITYZONE        test00
    INSTANCETYPE	Name         CPUs  Memory (MiB)  Disk (GiB)  NICs  Used / Total  Used %
    INSTANCETYPE	t1.micro        1           256           5     2     0 /     4      0%
    INSTANCETYPE	m1.small        1           256          10     2     0 /     4      0%
    INSTANCETYPE	m1.medium       1           512          10     2     0 /     4      0%
    INSTANCETYPE	c1.medium       2           512          10     2     0 /     2      0%
    INSTANCETYPE	m1.large        2           512          10     3     0 /     2      0%
    INSTANCETYPE	m1.xlarge       2          1024          10     4     0 /     2      0%
    INSTANCETYPE	c1.xlarge       2          2048          10     4     0 /     2      0%
    AVAILABILITYZONE        test01
    INSTANCETYPE	Name         CPUs  Memory (MiB)  Disk (GiB)  NICs  Used / Total  Used %
    INSTANCETYPE	t1.micro        1           256           5     2     0 /     4      0%
    INSTANCETYPE	m1.small        1           256          10     2     0 /     4      0%
    INSTANCETYPE	m1.medium       1           512          10     2     0 /     4      0%
    INSTANCETYPE	c1.medium       2           512          10     2     0 /     2      0%
    INSTANCETYPE	m1.large        2           512          10     3     0 /     2      0%
    INSTANCETYPE	m1.xlarge       2          1024          10     4     0 /     2      0%
    INSTANCETYPE	c1.xlarge       2          2048          10     4     0 /     2      0%

You are now ready to [](upgrade_from_oldv.dita) . 