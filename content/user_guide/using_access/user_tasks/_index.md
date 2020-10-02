+++
title = "Users"
weight = 5
chapter = true
+++


## Users
Users are subsets of accounts and are added to accounts by an appropriately credentialed administrator. While the term **user** typically refers to a specific person, in Eucalyptus, a **user** is defined by a specific set of credentials generated to enable access to a given account. Each set of user credentials is valid for accessing only the account for which they were created. Thus a user only has access to one account within a Eucalyptus system. If an individual person wishes to have access to more than one account within a Eucalyptus system, a separate set of credentials must be generated (in effect a new ‘user’) for each account (though the same username and password can be used for different accounts). 

When you need to add a new user to your Eucalyptus cloud, you'll go through the following process: 


| 1 | Create a user | 
| 2 | Add user to a group | 
| 3 | Give user a login profile | 

