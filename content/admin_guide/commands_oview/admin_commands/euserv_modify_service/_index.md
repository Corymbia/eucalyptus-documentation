+++
title = "euserv-modify-service"
weight = 10
+++


## Syntax


    euserv-modify-service -s STATE [-U URL] [--region USER@REGION]
    
       [-I KEY_ID] [-S KEY] [--security-token TOKEN]
       [--debug] [--debugger] [--version] [-h] SVCINSTANCE


## Positional Arguments


| Argument | Description | 
|  :---- |  :---- | 
| SVCINSTANCE | The name of the service instance to modify. | 


## Options


| Option | Description | Required | 
|  :---- |  :---- |  :---- | 
| -s, --state state | The state to change to. | Yes | 


## Output
No output is given. You can run the `euserv-describe-services` command to verify that the modification completed successfully, as shown in the example following. 


## Example
To modify the state of a storage controller service named "two-sc-1" to stopped: 



    euserv-modify-service -s stopped two-sc-1
    euserv-describe-services two-sc-1
    SERVICE  storage  two  two-sc-1  stopped  

