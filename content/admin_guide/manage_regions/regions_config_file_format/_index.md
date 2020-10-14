+++
title = "Region Configuration File Format"
weight = 20
+++

This section describes the necessary configuration properties that need to be addressed.For federation to be successfully configured, each cloud (i.e. region) that will be part of the federated cloud needs to have the following properties set (at a minimum): 

| Property Name | Description | 
|  :---- |  :---- | 
| region.region_name | This cloud property identifies the local region. This is required and should be valid for use in a DNS name. | 
| region.region_configuration | This property is a JSON document that will be the same for all federated regions. | 



