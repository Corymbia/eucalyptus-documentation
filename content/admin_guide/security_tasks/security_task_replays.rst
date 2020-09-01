+++
title = "Configure Replay Protection"
weight = 5
+++

..  _security_task_replays:

You can configure replay detection in Java components (which includes the CLC, UFS, OSG, Walrus, and SC) to allow replays of the same message for a set time period. 

{{% notice note %}}To protect against replay attacks, the Java components cache messages only for 15 minutes. So it’s important that any client tools used to interact with the components have the Expires element set to a value less than 15 minutes from the current time. This is usually not an issue with standard tools, such as euca2ools and Amazon EC2 API Tools. {{% /notice %}}The Java components' replay detection algorithm rejects messages with the same signatures received within 15 minutes. The time within which messages with the same signatures are accepted is controlled by the ``bootstrap.webservices.replay_skew_window_sec`` property. The default value of this property is 3 seconds. To change this value, enter the following command: 

.. code::

  euctl bootstrap.webservices.replay_skew_window_sec=[new_value_in_seconds]

If you set this property to ``0`` , Eucalyptus will not allow any message replays. This setting provides the best protection against message replay attacks. 

If you set this property to any value greater than 15 minutes plus the values of ws.clock_skew_sec (that is, to a value >= 920 sec in the default installation), Eucalyptus disables replay detection completely. 

When checking message timestamps for expiration, Eucalyptus allows up to 20 seconds of clock drift between the machines. This is a default setting. You can change this value for the Java components at runtime by setting the ``bootstrap.webservices.clock_skew_sec`` property as follows: 

.. code::

  euctl bootstrap.webservices.clock_skew_sec=[new_value_in_seconds]

