+++
title = "euserv-deregister-service"
weight = 5
+++

..  _euserv-deregister-service:



======
Syntax
======



.. code::

  euserv-deregister-service [-U URL] [--region USER@REGION] [-I KEY_ID]
  
         [-S KEY] [--security-token TOKEN] [--debug]
                [--debugger] [--version] [-h] SVCINSTANCE



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
    - Name of the service instance to de-register.




======
Output
======

Eucalyptus returns a message stating that service instance was successfully de-registered. 



=======
Example
=======

To de-register the dns service named "API_10.111.1.44.dns": 



.. code::

  euserv-deregister-service API_10.111.1.44.dns

