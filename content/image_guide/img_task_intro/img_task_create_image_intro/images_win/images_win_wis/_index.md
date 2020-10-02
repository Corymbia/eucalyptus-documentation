+++
title = "Install Eucalyptus Windows Integration"
weight = 10
hidden = true
+++

To install the Eucalyptus Windows Integration Service: 


{{% notice note %}}
The following step assumes you're running a recent version of Windows. If you're running Windows Server 2003, you'll need to download the legacy version of the Windows prep tool from: 
{{% /notice %}}
If you're running a version of Windows more recent than Windows Server 2003, download the most recent version of the Windows Image Preparation Tool from [http://downloads.eucalyptus.com/software/tools/windows-prep/](http://downloads.eucalyptus.com/software/tools/windows-prep/windows-prep-tools-latest.iso) to */var/lib/libvirt/images* on your NC. Open the libvirt-kvm-windows-example.xml file you used in the previous section and make the following edits: 

* Comment out the lines of XML code directing the hypervisor to boot the Windows image from the CDROM. 
* Change the text so that replaces the Windows .iso image and is mounted as . 
* Enter the path to the secondary disk file you created in the previous task. 
* Uncomment the lines that direct attachment of a floppy disk, secondary disk, and secondary network interface. 

{{% notice note %}}
If you plan on using virtio networking for instances (via USE_VIRTIO_NET option on node controllers), uncommenting the virtio interface in the xml is mandatory 
{{% /notice %}}
Your finished file should look similar to the following example: 


    <domain type="kvm">
    	  <name>eucalyptus-windows</name>
        <os>
        <type>hvm</type>
        <!-- <boot dev='cdrom'/> -->
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
            <disk type='file' device='disk'>
                 <source file='/var/lib/libvirt/images/secondary.img'/>
                 <target dev='vda' bus='virtio'/>
            </disk> 
            <disk type='file' device='floppy'>
                 <source file='/var/lib/libvirt/images/floppy.img'/>
                 <target dev='fda'/>
            </disk>
            <disk type='file' device='cdrom'>
                <source file='/var/lib/libvirt/images/windows-preps-tools-latest.iso'/>
                <target dev='hdc'/>
                <readonly/>
            </disk>
            <interface type='bridge'>
                <source bridge='br0'/>
                <model type='rtl8139'/>
            </interface>
            <interface type='bridge'>
                <source bridge='br0'/>
                <model type='virtio'/> 
            </interface>
            <graphics type='vnc' port='-1' autoport='yes' listen='0.0.0.0'/>
        </devices>
    </domain>

Start the VM. 
    cd /var/lib/libvirt/images/
    virsh create libvirt-kvm-windows-example.xml

Log in to Windows and find the Eucalyptus installation files in the CDROM drive. For Windows Server 2003 R2, run `setup.exe` . This automatically installs the .NET framework 2.0, which is not bundled in Server 2003 R2. For all other versions, run `EucalyptusWindowsIntegration.msi` . (setup.exe will automatically install .NET framework 2.0, which is not bundled in Server 2003 R2). In the Choose your hypervisor step, select KVM and then click Next . 
![image]({{< ref "/" >}}images/ewi_hypervisor.jpg)
Click Next and continue until the end of installation. 

Should this be a separate section, like Active Directory and Remote Desktop? Scot: maybe combine all into one process file of separate tasks. Reboot the Windows VM Open the Windows device manager and check that the following drivers are found for each device. 

* Floppy disk drive 
* Disk drivers: Red Hat VirtIO SCSI Disk Device 
* SCSI and RAID controllers: Red Hat VirtIO SCSI controller 
* Network adapters: Red Hat VirtIO Ethernet Adapter 
If the correct drivers are not found, question marks display on the devices. To install the devices, do the following: 

* Right-click on the devices in question and select to open the New Hardware Wizard. 
* When the new hardware wizard asks if Windows update is to be connected, click . 
* Choose . 
* If a confirmation popup message displays, click . 
