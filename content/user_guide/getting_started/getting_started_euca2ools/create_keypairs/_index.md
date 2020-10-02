+++
title = "Create Key Pairs"
weight = 10
hidden = true
+++

Eucalyptus uses cryptographic key pairs to verify access to instances. Key pairs are used if you want to connect to your instance using SSH. Creating a key pair generates two keys: a public key (saved within Eucalyptus) and a corresponding private key (output to the user as a character string). To enable this private key you must save it to a file and set appropriate access permissions (using the chmod command), as shown in the example below. 


## Create Key Pairs with the Console
From the main dashboard screen, click the Key Pairs icon. The Key Pairs page opens. Click the Create Key Pair button. The Create new key pair window opens. Type a name for the new key pair into the Name text box. The name may contain up to 255 alphanumeric and special characters. Click the Create and Download button. The private half of the key pair (.pem file) is saved to the default download location for your browser. 
{{% notice note %}}
Keep your private key file in a safe place. If you lose it, you will be unable to access instances created with the key pair. 
{{% /notice %}}
Change file permissions to enable access to the private key file in the local directory. For example, on a Linux or Mac OS X system: 
    chmod 0600 <keypair_name>.private


## Create Key Pairs with the Command Line
Enter the following command: 
    euca-create-keypair <keypair_name> -f <keypair_name>.private

where `<keypair_name>` is a unique name for your keypair. For example: 


    euca-create-keypair alice-keypair -f alice-keypair.private 

The private key is saved to a file in your local directory. Query the system to view the public key: 
    euca-describe-keypairs

The command returns output similar to the following: 
    KEYPAIR alice-keypair ad:0d:fc:6a:00:a7:e7:b2:bc:67:8e:31:12:22:c1:8a:77:8c:f9:c4

