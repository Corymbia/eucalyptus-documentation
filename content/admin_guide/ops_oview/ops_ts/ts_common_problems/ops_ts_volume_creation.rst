+++
title = "Problem: volume creation failed"
weight = 5
+++

..  _ops_ts_volume_creation:

Symptom: Went from available to fail. This is typically caused by the CLC and the SC.On the SC, use ``df`` or ``lvdisplay`` to check the disk space. Is there enough space? 

Yes: Check the `SC log <../troubleshooting-guide/ts_logs.dita>`_ and grep the volume ID. Is there error message? Yes. This provides clues to helpful information. No: Check `cloud-output.log <../troubleshooting-guide/ts_logs.dita>`_ for a volume ID error. No: Delete volumes or add disk space. 