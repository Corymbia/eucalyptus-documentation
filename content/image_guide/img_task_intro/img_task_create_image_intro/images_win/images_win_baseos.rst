+++
title = "Install Base Windows OS"
weight = 5
+++

..  _images_win_baseos:

The first task for creating a Windows image is installing a base Windows operating system (OS). To install a base Windows OS using KVM: 

Log in to the stopped NC server or a host that runs the same hypervisor as the NCs. Create a blank disk file. Specify your Windows VM image name using the parameter ``of`` . 

.. code::

  dd if=/dev/zero of=windows.<image_name>.img bs=1M count=1 seek=16999

{{% notice note %}}Your image name must start with the word, (all lower-case). {{% /notice %}}Create a floppy and secondary blank disk to be attached to the image later, in order to test paravirtualization drivers 

.. code::

  dd if=/dev/zero of=floppy.img \
  	bs=1k count=1474
  	dd if=/dev/zero of=secondary.img \
  	bs=1M count=1 seek=1000

Copy all of the .img and .iso files to the */var/lib/libvirt/images/* directory. Copy the *libvirt-kvm-windows-example.xml* file to your working directory and rename it to *libvirt-kvm-windows.xml* . 

.. code::

   cp /usr/share/eucalyptus/doc/libvirt-kvm-windows-example.xml /var/lib/libvirt/images/libvirt-kvm-windows.xml 

or 



.. code::

   cp /usr/share/eucalyptus/doc/libvirt-xen-windows-example.xml /var/lib/libvirt/images/libvirt-xen-windows.xml 

Open the new *libvirt-kvm-windows.xml* file and provide fully qualified paths to the VM image file and iso. Make sure that the name of the bridge is the same as the one used by the hypervisor on which you are creating the Windows image. Your file should look similar to the following example: 



.. code::

  <domain type='kvm'>
  	  <name>your-domain-name-here</name>
      <os>
      <type>hvm</type>
      <boot dev='cdrom'/>
      </os>
      <features>
          <acpi/>
      </features>
      <memory>524288</memory>
      <vcpu>1</vcpu>
      <devices>
          <emulator>/usr/libexec/qemu-kvm</emulator>
          <disk type='file'>
              <source file='/var/lib/libvirt/images/windows_2003.img'/>
              <target dev='hda'/>
          </disk>
          <!-- <disk type='file' device='disk'>
               <source file='fully_qualified_path_to_secondary_disk'/>
               <target dev='vda' bus='virtio'/>
          </disk> 
          <disk type='file' device='floppy'>
               <source file='fully_qualified_path_to_floppy_disk'/>
               <target dev='fda'/>
          </disk> -->
          <disk type='file' device='cdrom'>
              <source file='/var/lib/libvirt/images/en_win_srv_2003_r2_enterprise_with_sp2_cd1_x13-05460.iso'/>
              <target dev='hdc'/>
              <readonly/>
          </disk>
          <interface type='bridge'>
              <source bridge='br0'/>
              <model type='rtl8139'/>
          </interface>
          <!--<interface type='bridge'>
              <source bridge='br0'/>
              <model type='virtio'/> 
          </interface> -->
          <graphics type='vnc' port='-1' autoport='yes' listen='0.0.0.0'/>
      </devices>
  </domain>

Start the VM. 

.. code::

  cd /var/lib/libvirt/images
  virsh create libvirt-kvm-windows.xml

Connect to the virtual console using the VNC client of your choice. On the NC, check the display number that has been allocated by looking at the process table ( ``ps axw | grep vnc`` ). For example, if the display number is 0, then connect to the NC using the VNC client: 

.. code::

  vinagre <machine-hosting-vm>:0

Follow the standard Windows installation procedure until the VM has completed installing Windows. {{% notice note %}}On some hosts, the VNC’s display number will change when an image restarts. Use to find the current number. {{% /notice %}}Run ``virsh list`` to display the domain name. Shut down the Windows VM you have just created. The easiest way to shutdown your VM is to use the ``virsh destroy`` command, as shown: 

.. code::

  virsh destroy <domain_name>

