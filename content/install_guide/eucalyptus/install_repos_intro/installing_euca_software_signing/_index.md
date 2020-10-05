+++
title = "Software Signing"
weight = 10
+++

This topic describes Eucalyptus software signing keys.We use a number of GPG keys to sign our software packages and package repositories. The necessary public keys are provided with the relevant products and can be used to automatically verify software updates. You can also verify the packages or package repositories manually using the keys on this page. 

Use the `rpm --checksig` command on a download file to verify a RPM package for an Eucalyptus product. For example: 



    rpm --checksig -v myfilename.rpm



Follow the procedure detailed on Debian's [SecureApt](http://wiki.debian.org/SecureApt#How_to_manually_check_for_package.27s_integrity) web page to verify a deb package for an Eucalyptus product. 

Please do not use package signing keys to encrypt email messages. 

The following keys are used for signing Eucalyptus software: 


## c1240596: Eucalyptus Systems, Inc. (release key) <security@eucalyptus.com>
This key is used for signing Eucalyptus products released after July 2011 and their updates. 



* 
* 
* Fingerprint: 

## 0260cf4e: Eucalyptus Systems, Inc. (pre-release key) <security@eucalyptus.com>
This key is used for signing Eucalyptus pre-release products due for release after July 2011. 



* 
* 
* Fingerprint: 

## 9d7b073c: Eucalyptus Systems, Inc. (nightly release key) <security@eucalyptus.com>
This key is used for signing nightly builds of Eucalyptus products published after July 2011. 



* 
* 
* Fingerprint: 
