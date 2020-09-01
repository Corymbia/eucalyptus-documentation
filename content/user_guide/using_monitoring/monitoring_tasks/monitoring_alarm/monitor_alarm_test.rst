+++
title = "Test an Alarm"
weight = 5
+++

..  _monitor_alarm_test:

You can test the CloudWatch alarms by temporarily changing the state of your alarm to "ALARM" using the command: euwatch-set-alarm-state . 



.. code::

  euwatch-set-alarm-state --alarm-name TestAlarm --state ALARM

