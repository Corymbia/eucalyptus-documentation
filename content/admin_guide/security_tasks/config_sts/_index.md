+++
title = "Configure STS Actions"
weight = 10
+++

The Security Token Service (STS) allows you to enable or disable specific token actions.By default, the enabled actions list is empty. However, this means that all actions are enabled. To disable actions, list each action in the `disabledactions` property. To enable specific actions, list them in the `enabledactions` property. 



    # euctl tokens
    PROPERTY	tokens.disabledactions	{}
    PROPERTY	tokens.enabledactions	{}

The values for each property are case-insensitive, space or comma-separated lists of token service actions. If an action is in the disable list it will not be permitted. Eucalyptus returns an HTTP status 503 and the code `ServiceUnavailable` . 

If the enable list is not empty, Eucalyptus only permits the actions specifically listed. 



| Action | Description | 
|  :---- |  :---- | 
| AssumeRole | Roles as per AWS/STS and Eucalyptus-specific personas admin functionality | 
| GetAccessToken | Eucalyptus extension for password logins (for example, the Management Console) | 
| GetImpersonationToken | Eucalyptus extension that allows cloud administrators to act as specific users | 
| GetSessionToken | Session tokens in the sameas per AWS/STS | 

For more information about STS, go to [STS section of the AWS CLI Reference](http://docs.aws.amazon.com/cli/latest/reference/sts/index.html) . 

