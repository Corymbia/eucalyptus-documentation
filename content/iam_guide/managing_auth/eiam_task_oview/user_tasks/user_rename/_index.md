+++
title = "Modify a User"
weight = 60
+++

Modifying a user is similar to a "move" operation. To modify a user, you need permission to remove the user from the current path or name, and put that user in the new path or name.For example, if a user changes from one team in a company to another, you can change the user's path from */team_abc/* to */team_efg/* . You need permission to remove the user from */team_abc/* . You also need permission to put the user into */team_efg/* . This means you need permission to call UpdateUser on both *arn:aws:iam::123456789012:user/team_abc/** and *arn:aws:iam::123456789012:user/team_efg/** . 

To rename a user: 

Enter the following command to rename a user: 

    euare-usermod -u <user_name> --new-user-name <new_name>

Eucalyptus does not return a message. Enter the following command: 

    euare-groupmod -u <user_name> -p <new_path>

Eucalyptus does not return a message. 
