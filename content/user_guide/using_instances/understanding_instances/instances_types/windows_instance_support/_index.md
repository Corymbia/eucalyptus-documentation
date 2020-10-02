+++
title = "Windows Instance Support"
weight = 10
hidden = true
+++

Eucalyptus supports several different Windows operating system versions running as instances. Normal Windows licensing policies still apply. See the Compatibility Matrix in the Release Notes for supported versions. 

A VNC client is required during initial installation of the operating system but once Windows is fully installed, Remote Desktop Protocol can be used to connect to the Windows desktop. The VNC client is unnecessary if the Windows installation is configured as an unattended installation. As an example of one way to set up a Windows 7 unattended installation, see  [http://www.intowindows.com/how-to-create-unattended-windows-7-installation-setup](http://www.intowindows.com/how-to-create-unattended-windows-7-installation-setup) . 

All Windows images should be created on the hypervisor that runs on the Node Controllers.  Eucalyptus does not support running a Windows image across multiple hypervisors. The Eucalyptus Windows Integration software, installed in the Windows EMI, has a utility that adds permissions to users or groups that allows them to use RDP to access the Windows desktop.  By default, only the Administrator can do this. The Eucalyptus Windows Integration software also installs the Virtio device drivers for disk and network into the EMI so that it can run on a host configured with a KVM hypervisor. For more information about how to create a Windows image and install the Eucalyptus Windows Integration software, see the *Eucalyptus User Guide* . 

