+++
title = "euserv-describe-events"
weight = 5
+++

..  _euserv-describe-events:



======
Syntax
======



.. code::

  euserv-describe-events [-s] [-f FORMAT]



===========
Description
===========

Events come in the form of a list, where each event contains one or more of the following tags: 



.. list-table::
  :header-rows: 1

  *
    - Tag
    - Description
  *
    - id
    - A unique ID for the event.
  *
    - message
    - A free-form text description of the event.
  *
    - severity
    - The message's severity (FATAL, URGENT, ERROR, WARNING, INFO, DEBUG, TRACE).
  *
    - stack-trace
    - The stack trace, if any, corresponding to the event. The -s option is required to make this appear.
  *
    - subject-arn
    - The Eucalyptus ARN of the service affected by the event.
  *
    - subject-name
    - The name of the service affected by the event.
  *
    - subject-type
    - The type of service affected by the event.
  *
    - timestamp
    - The date and time of the event's creation.




===========
Environment
===========

{{% notice note %}}The command requires access keys and knowledge of where to locate the web services it needs to contact. It can obtain these from several locations. {{% /notice %}}

.. list-table::
  :header-rows: 1

  *
    - Environment
    - Description
  *
    - AWS_ACCESS_KEY_ID
    - The access key ID to use when authenticating web service requests. This takes precedence over and euca2ools.ini, but not -I.
  *
    - AWS_SECRET_ACCESS_KEY
    - The secret key to use when authenticating web service requests. This takes precedence over --region and euca2ools.ini(5), but not -S.
  *
    - EUCA_BOOTSTRAP_URL
    - The URL of the service to contact. This takes precedence over --region and euca2ools.ini, but not -U.




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
    - -f, --format format
    - Print events in a given format, where format can be: yaml or oneline, and format:string. See for details about each format. When omitted, the format defaults to yaml.` <{{< relref "" >}}>`__
    - No
  *
    - -s, --show-stack-traces
    - Include the stack-trace tag in events' data. This is omitted by default due to its length.
    - No




======
Output
======

There are several built-in formats, and you can define additional formats using a format: *string* , as described below. Here are the details of the built-in formats: 



**yaml**
	This outputs block-style YAML designed to be easily readable. Tags that are empty or not defined do not appear in this output at all. 

.. code::

  events:
              - timestamp: {timestamp}
              severity: {severity}
              id: {id}
              subject-type: {subject-type}
              subject-name: {subject-name}
              subject-host: {subject-host}
              subject-arn: {subject-arn}
              message: |-
              {message}
              stack-trace: |-
              {stack-trace}



**oneline**
	This output is designed to be as compact as possible. 

.. code::

  {timestamp} {severity} {subject-type} {subject-name} {message}



**format:string**
	The ``format:`` *string* format allows you to specify which information you want to show using placeholders enclosed in curly braces to indicate where to show the tags for each event. For example: 

.. code::

  euserv-describe-events -f "format:{timestamp} {subject-name} {message}"





=======
Example
=======

To output a list of service-affecting events in the ``oneline`` format: 



.. code::

  euserv-describe-events --format oneline
  2016-06-20 16:16:08 INFO node 10.111.1.15 the node is operating normally\nFound service status for 10.111.1.15: ENABLED
  2016-06-27 17:37:57 ERROR node 10.111.5.50 Error occurred in transport
  2016-06-28 07:00:17 ERROR node 10.111.5.50

