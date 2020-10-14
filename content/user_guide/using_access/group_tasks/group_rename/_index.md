+++
title = "Modify a Group"
weight = 30
+++

To modify a group perform the steps listed in this topic.Modifying a group is similar to a "move" operation. Whoever wants to modify the group must have permission to do it on both sides of the move. That is, you need permission to remove the group from its current path or name, and put that group in the new path or name. 

For example, if a group changes from one area in a company to another, you can change the group's path from */area_abc/* to */area_efg/* . You need permission to remove the group from */area_abc/* . You also need permission to put the group into */area_efg/* . This means you need permission to call `UpdateGroup` on both *arn:aws:iam::123456789012:group/area_abc/** and *arn:aws:iam::123456789012:group/area_efg/** . 

Enter the following command to modify the group's name: 

    euare-groupmod -g <group_name> --new-group-name <new_name>

Eucalyptus does not return a message. Enter the following command to modify a group's path: 

    euare-groupmod -g <group_name> -p <new_path>

Eucalyptus does not return a message. 
