+++
title = "Change a Tag's Value"
weight = 5
+++

..  _change_tag:

To change a tag's value: 

Enter the following command and parameters: 

.. code::

  euca-create-tags [resource]  --tag [key=value]

Eucalyptus returns a the resource identifier and its tag key and value. The following example changes the value of the stack tag for one of your EMIs from prod to test: 



.. code::

  euca-create-tags emi-1a2b3c4d  --tag stack=dev
  TAG  emi-1a2b3c4d  image  stack  dev

