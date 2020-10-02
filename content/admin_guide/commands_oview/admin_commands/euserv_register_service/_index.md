+++
title = "euserv-register-service"
weight = 10
hidden = true
+++


## Syntax

    euserv-register-service -t TYPE -h IP [--port PORT] [-z ZONE] [-U URL]
    
           [--region USER@REGION] [-I KEY_ID] [-S KEY]
               [--security-token   TOKEN]  [--debug]  [--debugger]  [--version]
               [--help] SVCINSTANCE


## Positional Arguments


| Argument | Description | 
|  :---- |  :---- | 
| SVCINSTANCE | The name of the new service instance to register. | 


## Options


| Option | Description | Required | 
|  :---- |  :---- |  :---- | 
| -t, --type type | The new service instance's type. | Yes | 
| -h, --host IP | The host on which the new instance of the service runs. | Yes | 
| --port port | The port on which the new instance of the service runs (default for cluster: 8774, otherwise: 8773). | No | 
| -z, --availability-zone zone | The availability zone in which to register the new service instance. This is required only for services of certain types. | Conditional | 


## Output
No output is given when it succeeds. 


## Example
To register the ufs service named "user-api-5": 


    euserv-register-service -t user-api -h 10.0.0.15 user-api-5


{{% notice note %}}
A prerequisite for this command is to have the credentials in the shell you are running the register command. For example: 
{{% /notice %}}
