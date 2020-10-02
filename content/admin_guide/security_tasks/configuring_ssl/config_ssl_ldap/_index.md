+++
title = "Configure SSL for LDAP"
weight = 5
+++

This topic details tasks required to configure SSL for LDAP.To configure SSL for LDAP, make the following edits to your LIC template or file. 


{{% notice note %}}
For more information about the LIC template and file, see . 
{{% /notice %}}
Edit the `use-ssl` value to `true` . 
    "use-ssl":"true",

Edit the `ignore-ssl-cert-validation` value to `false` . 
    "ignore-ssl-cert-validation":"false",

