+++
title = "Images and Instances"
weight = 10
+++

Because all instances are based on images, creating a secure image helps to create secure instances. This topic lists best practices that will add additional security during image creation. As a general rule, harden your images similar to how you would harden your physical servers.

* Turn off password-based authentication by specifying the following option in : 
* Encourage non-root access by providing an unprivileged user account. If necessary, use sudo to allow access to privileged commands 
* Always delete the shell history and any other potentially sensitive information before bundling. If you attempt more than one bundle upload in the same image, the shell history contains your secret access key. 
* Bundling a running instance requires your private key and X.509 certificate. Put these and other credentials in a location that is not bundled (e.g. when using , pass the folder location where the certificates are stored as part of the values for the option). AWS provides more in-depth information on . 
* Consider installing in the image to help control root and non-root access. If cloud-init isn't available, a custom script can be used. 
* Consider using a tool such as zerofree to zero-out any unused space on the image. 
* Consider editing to clear out the swap every time the instance is booted. This can be done using the following command: 
* Consider enabling or for your images 
* Disable all unused services and ports on the image. 
* By default, all images registered have private launch permissions. Consider using to limit the accounts that can access the image. 
After locking down the image using the steps above, additional steps can be done to further secure instances started from that image. For example, restrict access to the instance by allowing only trusted hosts or networks to access ports on your instances. You can control access to instances using `euca-authorize` and `euca-revoke` . 

Consider creating one security group that allows external logins and keep the remainder of your instances in a group that does not allow external logins. Review the rules in your security groups regularly, and ensure that you apply the principle of least privilege: only open up permissions as they are required. Use different security groups to deal with instances that have different security requirements. 

