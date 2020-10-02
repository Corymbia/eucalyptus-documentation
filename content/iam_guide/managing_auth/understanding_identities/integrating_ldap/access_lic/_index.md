+++
title = "LDAP/AD Integration Configuration"
weight = 5
chapter = true
+++


## LDAP/AD Integration Configuration
The LDAP/AD Integration Configuration (LIC) is a JSON format file. This file specifies everything Eucalyptus needs to know about how to synchronize with an LDAP or AD service.You can find a LIC template at */usr/share/eucalyptus/lic_template* . This template shows all the fields of the LIC, and provides detailed documentation and example values for each field. 

To start a LIC file, use the LIC command line tool. 


    /usr/sbin/euca-lictool --password <password> --out example.lic

The above command invokes the LIC tool to create a template LIC and fill in the encrypted password for authenticating to LDAP/AD service (i.e. the password of the administrative user for accessing the LDAP/AD during synchronization). The LIC tool’s primary functions are to encrypt the LDAP/AD password and to generate the starting LIC template. The usage of the LIC tool shows different ways to invoke the command. 

Once you have the LIC template, you can fill in the details by editing the “*.lic” file using your favorite editor as it is a simple text file. As we said above, the LIC file is in JSON format. Each top level entity specifies one aspect of the LDAP/AD synchronization. The following shows one possible example of a LIC file. 


    {
    "ldap-service":{
      "server-url":"ldap://localhost:7733",
      "auth-method":"simple",
      "user-auth-method":"simple",
      "auth-principal":"cn=ldapadmin,dc=foo,dc=com",
      "auth-credentials": "{RSA/ECB/PKCS1Padding}EAXRnvwnKtCZOxSrD/F3ng/yHH3J4jMxNUS
      kJJf6oqNMsUihjUerZ20e5iyXImPgjK1ELAPnppEfJvhCs7woS7jtFsedunsp5DJCNhgmOb2CR/MnH
      11V3FNY7bBWoew5A8Wwy6x7YrPMS0j7dJkwM7yfp1Z6AbKOo2688I9uIvJUQwEKS4dOp7RVdA0izlJ
      BDPAxiFZ2qa40VjFI/1mggbiWDNlgxiVtZXAEK7x9SRHJytLS8nrNPpIvPuTg3djKiWPVOLZ6vpSgP
      cVEliP261qdUfnf3GDKi3jqbPpRRQ6n8yI6aHw0gAtq8/qPyqjkkDP8JsGBgmXMxiCNPogbWg==",
      "use-ssl":"false",
      "ignore-ssl-cert-validation":"false",
      "krb5-conf":"/path/to/krb5.conf",
    },
    
    "sync":{
      "enable":"true",
      "auto":"true",
      "interval":"900000",
      "clean-deletion":"false",
    },
    
    "accounting-groups":{
      "base-dn":"ou=groups,dc=foo,dc=com",
      "id-attribute":"cn",
      "member-attribute":"member",
      "selection":{
          "filter":"objectClass=accountingGroup",
          "select":["cn=accountingToSelect,ou=Groups,dc=foo,dc=com"],
          "not-select":["cn=accountingToIgnore,ou=Groups,dc=foo,dc=com"],
      }
    },
    
    "groups":{
      "base-dn":"ou=groups,dc=foo,dc=com",
      "id-attribute":"cn",
      "member-attribute":"member",
      "selection":{
          "filter":"objectClass=groupOfNames",
          "select":["cn=groupToSelect,ou=Groups,dc=foo,dc=com"],
          "not-select":["cn=groupToIgnore,ou=Groups,dc=foo,dc=com"],
      }
    },
    
    "users":{
      "base-dn":"ou=people,dc=foo,dc=com",
      "id-attribute":"uid",
      "user-info-attributes":{
          "fullName":"Full Name",
          "email":"Email"
      },
      "selection":{
          "filter":"objectClass=inetOrgPerson",
          "select":["uid=john,ou=People,dc=foo,dc=com", "uid=jack,ou=People,dc=foo,dc=com"],
          "not-select":["uid=tom,ou=People,dc=foo,dc=com"],
      }
    },

In the following sections explain each field of LIC in detail. 

