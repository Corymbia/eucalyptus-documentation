+++
title = "Add a User"
weight = 5
+++

..  _user_add:

To add a user, perform the steps in this topic.Enter the following command 

.. code::

  euare-usercreate -u <user_name> -g <group_name> -k

Eucalyptus does not return a response. {{% notice note %}}If you include the parameter, Eucalyptus returns a response that includes the user's ARN and GUID. {{% /notice %}}