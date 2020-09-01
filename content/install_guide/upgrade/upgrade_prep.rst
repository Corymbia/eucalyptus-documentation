+++
title = "Prepare for Upgrade"
weight = 5
+++

..  _upgrade_prep:

This topic helps you prepare for upgrading Eucalyptus .**Prerequisites** Before starting the upgrade, ensure that you have: 



* Verified that your hardware and software are compatible with . 

* Verified the health of your current deployment, as described in in the . 

* Followed the of prior versions, if needed, to prepare for this upgrade. 

* Backed up your data and followed best practices for your environment. See . See also in the . 

* Prepared to upgrade . does not support services that are on different release versions. For example, you cannot have a CLC at and a Walrus at . 

* Verified that you already have the repositories installed for Euca2ools and EPEL from your previous installation. If you do not have these installed, see the installation instructions for that version's Installation Guide in the to find out how to add these to your host machines. 

* Fully updated your existing (pre- ) services using where possible. 

* Removed any hand-written repository files for earlier versions of and Euca2ools from . 

{{% notice note %}}{{% /notice %}}{{% notice note %}}You can preview the install and its dependencies by running the following commands. {{% /notice %}}**To preview the upgrade of Eucalyptus cloud** 

The following steps are an optional preview of what the upgrade command will do. If you do not want to do this, continue to ` <upgrade_shutdown.dita>`_ . 

(Optional) Test the new Eucalyptus release package on each host machine that runs a Eucalyptus service: 

.. code::

  yum install 

Review the dependencies and install package information. 

Enter ``N`` when prompted so you do **NOT** install the package. 

(Optional) Test the new Euca2ools release package on each host machine that runs Euca2ools or a Eucalyptus service: 

.. code::

  yum install 

Review the dependencies and install package information. 

Enter ``N`` when prompted so you do **NOT** install the package. 

(Optional) If you have a Eucalyptus subscription, test the new subscription release package on each host machine that runs a Eucalyptus service: 

.. code::

  yum install 

Review the dependencies and install package information. 

Enter ``N`` when prompted so you do **NOT** install the package. 

You are now ready to ` <upgrade_shutdown.dita>`_ . 