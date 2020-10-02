+++
title = "Management Console"
weight = 10
+++

This topic describes things you can do to secure the Eucalyptus Management Console.

* Enable HTTPS for communications with the console and configure the console to use a CA-signed certificate. 
* We do not recommend the "Remember my keys" option for "Login to AWS" because it stores AWS credentials in your browser's local storage and increases the security risk of AWS credentials being compromised. 
* Change the default session timeouts if needed. For more information, see . 
* If you don't use the Management Console, we recommend that you disable (using ). For more information, see . 
* Turn off password autocomplete for the console by setting the configuration option to false in the console’s configuration file. 
* If memcached is configured to be used by the console, make sure it’s not exposed publicly because there is no authentication mechanism enabled out of the box. If the default Eucalyptus-provided configuration is used, it accepts connections only from localhost. 
