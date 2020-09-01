+++
title = "Delete a Group"
weight = 5
+++

..  _group_delete:

To delete a group perform the steps listed in this topic.When you delete a group, you have to remove users from the group and delete any policies from the group. You can do this with one command, using the ``euare-groupdel`` command with the ``-r`` option. Or you can follow the following steps to specify who and what you want to delete. 

Individually remove all users from the group. 

.. code::

  euare-groupremoveuser -g <group_name> -u <user_name>

Delete the policies attached to the group. 

.. code::

  euare-groupdelpolicy -g <group_name> -p <policy_name>

Delete the group. 

.. code::

  euare-groupdel -g <group_name>

The group is now deleted. 