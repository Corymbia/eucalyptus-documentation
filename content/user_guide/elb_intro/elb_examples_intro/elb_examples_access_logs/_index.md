+++
title = "Accessing Load Balancer Logs"
weight = 120
+++

To help analyze an application’s performances or troubleshoot problems, you can capture detailed information for all requests coming through your load balancers. When enabled, such access logs will be captured and stored in the S3 bucket.To access ELB logs: 

Before enabling the access logs, update the access control of your S3 (Eucalyptus object-storage-gateway) bucket so that Eucalyptus’ load balancer has write permissions. The access control list requires the canonical ID of the grantee. To obtain the canonical ID of the load balancing service: 
{{% notice note %}}
If your cloud is using VPCMIDO networking mode, use the command in the next step. 
{{% /notice %}}


    eulb-describe-lbs --show-long --region devops-admin@region-1
    LOAD_BALANCER myloadbalancer	
    myloadbalancer-000476918024.lb.a-18.autoqa.qa1.eucalyptus-systems.com			
    {interval=30,target=TCP:80,timeout=5,healthy-threshold=3,unhealthy-threshold=3	
    cash,money i-6f2a1874,i-be660343	
    {protocol=HTTP,lb-port=80,instance-protocol=HTTP,instance-port=80}					
    {owner-alias=000865102303,group-name=euca-internal-000476918024-myloadbalancer}		
    2015-09-29T18:11:33.761Z	
    internet-facing


{{% notice note %}}
Save the number at the end of the output to update the bucket's ACL in . 
{{% /notice %}}


To obtain the canonical ID of the load balancing service in VPCMIDO networking mode: 
{{% notice note %}}
If your cloud is not using VPCMIDO networking mode, use the command in the previous step. 
{{% /notice %}}


    euserv-describe-services --filter service-type=loadbalancing --expert
    SERVICE arn:euca:bootstrap:API_10.111.1.19:loadbalancing:API_10.111.1.19.loadbalancing/ enabled 25 
    http://10.111.1.19:8773/services/LoadBalancing 
    (eucalyptus)loadbalancing=000036660381:28323c32338354b20255a633830524c1224434cb1a5254c1d614614841586042


{{% notice note %}}
Save the number at the end of the output to update the bucket's ACL in . 
{{% /notice %}}


Use any S3 client tools to update the bucket’s ACL. For example: 

    # aws --endpoint-url http://objectstorage.a-18.autoqa.qa1.eucalyptus-systems.com:8773/ s3 s3://webserverlog
    # aws --endpoint-url http://objectstorage.a-18.autoqa.qa1.eucalyptus-systems.com:8773/ s3api put-bucket-acl --grant-write "id=000865102303" --bucket s3://webserverlog

Modify your load balancer’s attributes to enable the access logs. For example: 

    eulb-modify-lb-attributes myloadbalancer AccessLog.Enabled=true AccessLog.S3BucketName=webserverlog AccessLog.EmitInterval=5 AccessLog.S3BucketPrefix=myprefix

Check that the attribute has been updated correctly by using the `eulb-describe-lb-attributes` command: 

    eulb-describe-lb-attributes myloadbalancer
    AccessLog.EmitInterval  5
    AccessLog.Enabled true
    AccessLog.S3BucketName  webserverlog
    AccessLog.S3BucketPrefix  myprefix
    ConnectionDraining.Enabled  false
    ConnectionSettings.IdleTimeout 60
    CrossZoneLoadBalancing.Enabled true      

