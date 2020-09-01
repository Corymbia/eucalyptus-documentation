+++
title = "euserv-modify-service"
weight = 5
+++

..  _euserv-modify-service:



======
Syntax
======



.. code::

  euserv-modify-service -s STATE [-U URL] [--region USER@REGION]
  
     [-I KEY_ID] [-S KEY] [--security-token TOKEN]
     [--debug] [--debugger] [--version] [-h] SVCINSTANCE



====================
Positional Arguments
====================



.. list-table::
  :header-rows: 1

  *
    - Argument
    - Description
  *
    - SVCINSTANCE
    - The name of the service instance to modify.




=======
Options
=======



.. list-table::
  :header-rows: 1

  *
    - Option
    - Description
    - Required
  *
    - -s, --state state
    - The state to change to.
    - Yes




======
Output
======

No output is given. You can run the ``euserv-describe-services`` command to verify that the modification completed successfully, as shown in the example following. 



=======
Example
=======

To modify the state of a storage controller service named "two-sc-1" to stopped: 



.. code::

  euserv-modify-service -s stopped two-sc-1
  euserv-describe-services two-sc-1
  SERVICE  storage  two  two-sc-1  stopped  

