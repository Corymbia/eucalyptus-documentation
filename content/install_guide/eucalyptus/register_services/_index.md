+++
title = "Register Eucalyptus Services"
weight = 60
chapter = true
+++


# Register Services
This section describes how to register Eucalyptus services.

{{% notice note %}}
If you are upgrading, proceed to the section. (You don't need to register the rest (e.g., UFS, Walrus, etc.) during the non-NC upgrade, because those registrations are already listed in the cloud database, which you recovered before getting here.) 
{{% /notice %}}

Eucalyptus implements a secure protocol for registering separate services so that the overall system cannot be tricked into including a service run by an unauthorized administrator or user. 

You need only register services once. Most registration commands run on the CLC server. 

Note that each registration command will attempt an SSH as root to the remote physical host where the registering service is assumed to be running. The registration command also contacts the service so it must be running at the time the command is issued. If a password is required to allow SSH access, the command will prompt the user for it. 

Registration commands need the following information:

* The of service you are registering. Required. For example: . 
* The of the service being registered. Required. The host must be specified by IP address to function correctly. 
* The the service belongs to. This is roughly equivalent to the availability zone in AWS. 
* The you assign to each instance of a service, up to 256 characters. Required. This is the name used to identify the service in a human-friendly way. This name is also used when reporting system state changes that require administrator attention. 


{{% children sort="weight" %}}
