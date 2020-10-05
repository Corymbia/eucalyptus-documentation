+++
title = "euserv-describe-services"
weight = 10
+++


## Syntax


    euserv-describe-services [-a]
    
           [--group-by-type | --group-by-zone | --group-by-host | --expert]
             [--show-headers]   [--show-empty-fields]   [-U   URL]  [--region
             USER@REGION]  [-I  KEY_ID]  [-S  KEY]  [--security-token  TOKEN]
             [--filter  NAME=VALUE]  [--debug]  [--debugger] [--version] [-h]
             [SVCINSTANCE [SVCINSTANCE ...]]


## Positional Arguments


| Argument | Description | 
|  :---- |  :---- | 
| SVCINSTANCE | Limit results to specific instances of services. | 


## Options


| Option | Description | Required | 
|  :---- |  :---- |  :---- | 
| -a, --all | Show all services regardless of type. | No | 
| --group-by-type | Collate services by service type (default). | No | 
| --group-by-zone | Collate services by availability zone. | No | 
| --group-by-host | Collate services by host. | No | 
| --expert | Show advanced information, including service accounts. | No | 
| --show-headers | Show column headers. | No | 
| --filter name=value | Restrict results to those that meet criteria. Allowed filter names: availability-zone. The service's availability zone.host. The machine running the service.internal. Whether the service is used only internally (true or false).public. Whether the service is public (true or false).service-group. Whether the service is a member of a specific service group.service-group-member. Whether the service is a member of any service group (true or false).service-type. The type of service.state. The service's state. | No | 


## Output
Eucalyptus returns information about the services you specified. 


## Example
Verify that you are looking at the cloud controllers view of the service state by explicitly running against that host: 



    euserv-describe-services --filter service-type=storage -U http://localhost:8773/services/Empyrean
    SERVICE  storage  one  one-sc-1  enabled

