+++
title = "Start a LIC File"
weight = 10
+++

To start a LIC file perform the steps listed in this topic.The LIC is a file in JSON format, specifying everything Eucalyptus needs to know about how to synchronize with an LDAP or AD service. Eucalyptus provides a LIC template at *${EUCALYPTUS}/usr/share/eucalyptus/lic_template* . This template shows all the fields of the LIC, and provides detailed documentation and example values for each field. 

To start a LIC file: 

Enter the following command: 

    /usr/sbin/euca-lictool --password secret --out example.lic

The above command invokes the LIC tool to create a template LIC and fill in the encrypted password for authenticating to LDAP/AD service (i.e. the password of the administrative user for accessing the LDAP/AD during synchronization). The LIC tool’s primary functions are to encrypt the LDAP/AD password and to generate the starting LIC template. The usage of the LIC tool shows different ways to invoke the command. Once you have the LIC template, you can fill in the details by editing the **.lic* file using a text editor. Each top level entity specifies one aspect of the LDAP/AD synchronization. 