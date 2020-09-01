+++
title = "Start a LIC File"
weight = 5
+++

..  _security_task_ldap:

The LIC is a file in JSON format and specifies what Eucalyptus needs for synchronizing with an LDAP or AD service. Eucalyptus provides a LIC template at . This template shows all the fields of the LIC, and provides detailed documentation and example values for each field.To start a LIC file: 

Enter the following command: 

.. code::

  /usr/sbin/euca-lictool --password secret --out example.lic

This command tells the LIC tool to create a template LIC and fill in the encrypted password for authenticating to LDAP/AD service (that is, the password of the administrative user for accessing the LDAP/AD during synchronization). The LIC tool’s primary functions are to encrypt the LDAP/AD password and to generate the starting LIC template. The usage of the LIC tool shows different ways to invoke the command. Once you have the LIC template, fill in the details by editing the *.lic* file using a text editor. Each top level entity specifies one aspect of the LDAP/AD synchronization. 
