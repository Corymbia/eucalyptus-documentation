+++
title = "About Eucanetd"
weight = 5
+++

..  _eucanetd_about:

The eucanetd service implements artifacts to manage and define Eucalyptus cloud networking. Eucanetd runs alongside the CLC, CC, and/or NC services, depending on the configured networking mode.Eucanetd manages network functionality. For example: 

* Installs network artifacts (iptables, ipsets, ebtables, dhcpd) 

* Performs state management for the installed network artifacts 

* Maintains the eucanetd.log file 

* Updates network artifact configuration as needed 

* In VPCMIDO mode: 





========================
Where to deploy eucanetd
========================

On a Eucalyptus 4.4 cloud: 



.. list-table::
  :header-rows: 1

  *
    - Host Machine
    - EDGE mode
    - VPCMIDO mode
  *
    - CLC
    - No
    - Only on CLC
  *
    - CC
    - No
    - No
  *
    - NC
    - On each NC
    - No


REMOVE THE FOLLOWING TABLE in 5.0. DOC-1888 On a Eucalyptus 4.3 cloud: 



.. list-table::
  :header-rows: 1

  *
    - Host Machine
    - EDGE mode
    - MANAGED modes (deprecated)
    - VPCMIDO mode
  *
    - CLC
    - No
    - No
    - Only on CLC
  *
    - CC
    - No
    - On each CC
    - No
  *
    - NC
    - On each NC
    - On each NC
    - No


