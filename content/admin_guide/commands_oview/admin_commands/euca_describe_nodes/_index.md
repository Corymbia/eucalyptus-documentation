+++
title = "euserv-describe-node-controllers"
weight = 10
+++


## Syntax


    euserv-describe-node-controllers [--ec2-url URL] [--show-headers]
    
       [--show-empty-fields] [-U URL]
              [--region USER@REGION] [-I KEY_ID]  [-S  KEY]  [--security-token
              TOKEN] [--debug] [--debugger] [--version] [-h]


## Options


| Option | Description | Required | 
|  :---- |  :---- |  :---- | 
| --ec2-url url | The compute service's endpoint URL. | No | 
| --show-headers | Show column headers. | No | 


## Output
Eucalyptus returns information about the node controller and its instances, for example: 

    NODE  one  10.111.1.53  enabled    
    INSTANCE  i-162a8f09      
    INSTANCE  i-2b6cdd10      
    NODE  one  10.111.5.132  enabled    
    INSTANCE  i-ba9307d7




## Example


    euserv-describe-node-controllers --region localhost

