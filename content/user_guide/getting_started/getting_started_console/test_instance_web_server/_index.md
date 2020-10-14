+++
title = "Set Up A Web Server on an Instance"
weight = 30
+++

Once you've launched an instance and connected to it, you can test it by setting up a web server. 

ssh into your instance. 

    ssh 192.168.1.1 -l root

Install Apache: 

    yum install -y httpd

You should see output similar to the following: 

    Loaded plugins: fastestmirror, security, versionlock
    Loading mirror speeds from cached hostfile
     * extras: centos.sonn.com
    centos-7-x86_64-os                                       | 3.7 kB     00:00
    centos-7-x86_64-updates                                  | 3.4 kB     00:00
    centos-7-x86_64-updates/primary_db                       | 5.4 MB     00:00
    epel-7-x86_64                                            | 4.4 kB     00:00
    epel-7-x86_64/primary_db                                 | 6.3 MB     00:00
    extras                                                   | 3.3 kB     00:00
    Setting up Install Process
    Package httpd-2.2.15-31.el7.centos.x86_64 already installed and latest version
    Nothing to do

Start the web server: 

    systemctl start httpd.service

You should see output similar to the following: 



    Starting httpd:                                            [  OK  ]

Test connectivity to your instance by using a web browser and connecting to the web service on your instance. For example: 


![image]({{< ref "/" >}}images/test_instance_web_server_connect.png)
