+++
title = "euserv-migrate-instances"
weight = 10
+++


## Syntax


    euserv-migrate-instances (-s HOST | -i INSTANCE)
    
      [--include-dest HOST | --exclude-dest HOST]
      [-U URL] [--region USER@REGION] [-I KEY_ID]  [-S  KEY]  [--security-token
      TOKEN] [--debug] [--debugger] [--version] [-h]


## Options


| Option | Description | Required | 
|  :---- |  :---- |  :---- | 
| -s, --source host | Remove all instances from a specific host. | No | 
| -i, --instance instance | Remove one instance from its current host. | No | 
| --include-dest host | Allow migration to only a specific host (may be used more than once). | No | 
| --exclude-dest host | Allow migration to any host except a specific one (may be used more than once). | No | 


## Output
Unless requested, no output is given. You can run the `euserv-describe-*` command to verify that the migration activity completed successfully, as shown in the example following. 


## Example
To migrate an instance from its current host: 



    euserv-migrate-instances -i i-8eacd211 
    euserv-describe-node-controllers 
    NODE  zone-555  10.104.1.200  enabled    
    
    NODE  zone-555  10.104.1.201  enabled    
    INSTANCE  i-8eacd211      

