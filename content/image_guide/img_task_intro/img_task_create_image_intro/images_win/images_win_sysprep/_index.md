+++
title = "Run Sysprep"
weight = 10
+++

Sysprep is a Microsoft tool for deploying multiple Windows operating systems in an enterprise. Running Sysprep removes system-specific information such as security ID (SID) from the Windows OS before you clone an image. Sysprep then re-initializes the OS after the image is cloned and started on multiple computers. Use Sysprep to prepare images when you use Microsoft Key Management Service to activate license keys. Also, use Sysprep when your Windows systems are attached to Active Directory. 

In Eucalyptus, you can run Sysprep before you bundle images with the `euca-bundle-image` or `euca-bundle-instance` commands. 


{{% notice note %}}
The Eucalyptus Integration Service supports Sysprep for Windows Server 2008, Windows Server 2008 R2, and Windows 7. 
{{% /notice %}}
To configure and run Sysprep: 

Open the Eucalyptus Windows Integration popup ( Windows Programs Eucalyptus Eucalyptus Setup ). 
![image]({{< ref "/" >}}images/ewi_gen.jpg)
Click the General tab. Ensure that Format uninitialized drives is checked If you want to edit the Sysprep answer file, click the Open and change button in the General tab. Otherwise skip this step. Click the Run Sysprep button. Sysprep starts. After Sysprep is complete, close the application and shutdown the Windows VM using the Windows Programs menu. 