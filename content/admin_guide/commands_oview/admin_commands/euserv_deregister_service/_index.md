+++
title = "euserv-deregister-service"
weight = 10
+++


## Syntax


    euserv-deregister-service [-U URL] [--region USER@REGION] [-I KEY_ID]
    
           [-S KEY] [--security-token TOKEN] [--debug]
                  [--debugger] [--version] [-h] SVCINSTANCE


## Positional Arguments


| Argument | Description | 
|  :---- |  :---- | 
| SVCINSTANCE | Name of the service instance to de-register. | 


## Output
Eucalyptus returns a message stating that service instance was successfully de-registered. 


## Example
To de-register the dns service named "API_10.111.1.44.dns": 



    euserv-deregister-service API_10.111.1.44.dns

