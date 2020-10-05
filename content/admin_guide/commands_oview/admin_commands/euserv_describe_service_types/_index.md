+++
title = "euserv-describe-service-types"
weight = 10
+++


## Syntax


    euserv-describe-service-types [-a] [--show-headers]
    
    [--show-empty-fields] [-U URL]
       [--region  USER@REGION]  [-I  KEY_ID]  [-S  KEY] [--security-token TOKEN]
       [--debug] [--debugger] [--version] [-h]


## Options


| Option | Description | Required | 
|  :---- |  :---- |  :---- | 
| -a, --all | Show all service types regardless of their properties. | No | 
| --show-headers | Show column headers. | No | 


## Output
Eucalyptus returns a list of service types. 


## Example


    euserv-describe-service-types 
    SVCTYPE  arbitrator                The Arbitrator service                                      
    SVCTYPE  autoscaling     user-api  Auto Scaling API service                                    
    SVCTYPE  cloudformation  user-api  Cloudformation API service                                  
    SVCTYPE  cloudwatch      user-api  CloudWatch API service                                      
    SVCTYPE  cluster                   The Cluster Controller service                              
    SVCTYPE  compute         user-api  the Eucalyptus EC2 API service                              
    SVCTYPE  dns             user-api  Eucalyptus DNS server                                       
    SVCTYPE  euare           user-api  IAM API service                                             
    SVCTYPE  eucalyptus                eucalyptus service implementation                           
    SVCTYPE  identity        user-api  Eucalyptus identity service                                 
    SVCTYPE  imaging         user-api  Eucalyptus imaging service                                  
    SVCTYPE  loadbalancing   user-api  ELB API service                                             
    SVCTYPE  objectstorage   user-api  S3 API service                                              
    SVCTYPE  simpleworkflow  user-api  Simple Workflow API service                                 
    SVCTYPE  storage                   The Storage Controller service                              
    SVCTYPE  tokens          user-api  STS API service                                             
    SVCTYPE  user-api                  The service group of all user-facing API endpoint services  
    SVCTYPE  walrusbackend             The legacy Walrus Backend service



