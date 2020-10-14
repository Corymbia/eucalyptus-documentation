+++
title = "Add a Group Policy"
weight = 20
+++

To add a group policy perform the steps listed in this topic.Enter the following command: 

    euare-groupaddpolicy -g <group_name> -p <policy_name> -e <effect> -a
    							<actions> -o

The optional `-o` parameter tells Eucalyptus to return the JSON policy, as in this example: 

    {"Version":"2008-10-17","Statement":[{"Effect":"Allow", "Action":["ec2:RunInstances"], "Resource":["*"]}]}

