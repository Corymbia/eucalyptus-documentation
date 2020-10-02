+++
title = "Problem: install-time checks"
weight = 10
+++

Eucalyptus offers installation checks for any Eucalyptus component or service (CLC, Walrus, SC, NC, SC, services, and more). When Eucalyptus encounters an error, it presents the problem to the operator. These checks are used for install-time problems. They provide resolutions to some of the fault conditions. 

Each problematic condition contains the following information: 



| Heading | Description | 
|  :---- |  :---- | 
| Condition | The fault found by Eucalyptus | 
| Cause | The cause of the condition | 
| Initiator | What is at fault | 
| Location | Where to go to fix the fault | 
| Resolution | The steps to take to resolve the fault | 


![image]({{< ref "/" >}}images/install-check.png)


For more information about all the faults we support, go to [https://github.com/eucalyptus/eucalyptus/tree/master/util/faults/en_US](https://github.com/eucalyptus/eucalyptus/blob/master/util/README.faults) . 

