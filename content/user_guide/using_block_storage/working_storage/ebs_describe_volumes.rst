+++
title = "List Available EBS Volumes"
weight = 5
+++

..  _ebs_describe_volumes:

You can use the Eucalyptus command line tools to list all available volumes and retrieve information about a specific volume. 

To get a list of all available volumes in your Eucalyptus cloud, enter the following command: 

.. code::

  euca-describe-volumes

To get information about one specific volume, use the ``euca-describe-volumes`` command and specify the volume ID. 

.. code::

  euca-describe-volumes vol-00000000

