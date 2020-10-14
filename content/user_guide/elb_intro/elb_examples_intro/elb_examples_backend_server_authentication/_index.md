+++
title = "Configuring Back-end Server Authentication"
weight = 100
+++

When running a web application with HTTPS or SSL as the backend server’s protocol, you might want to authenticate the back-end servers using the public key of the back-end server’s certificate. This authentication can be used to ensure that back-end servers accept only encrypted communication and to ensure that the back-end servers have the correct certificate.To configure back-end server authentication: 

Create a new loadbalancer with HTTPS as backend instance’s protocol: 

    eulb-create-lb -l "protocol=HTTPS,lb-port=443,instance-protocol=HTTPS,instance-port=8443,cert-id=arn:aws:iam::000550595745:server-certificate/mycert01"\
                            -z one myloadbalancer

Create a new PublicKeyPolicyType policy for the load balancer. In the example below, ‘server.crt’ is the file containing the public key of the backend server’s certificate. 

    eulb-create-lb-policy -n webservercert -t PublicKeyPolicyType -a "name=PublicKey, value=$(<./server.crt)" myloadbalancer

Use the `eulb-describe-lb-policies` to ensure that the policy was created. For example: 

    eulb-describe-lb-policies -p webservercert myloadbalancer

Create a new `BackendServerAuthenticationPolicyType` policy that refers to the public key policy created above. 

    eulb-create-lb-policy -n webserverauthentication -t BackendServerAuthenticationPolicyType -a "name=PublicKeyPolicyName, value=webservercert" myloadbalancer

Make sure the policy is created. For example: 

    eulb-describe-lb-policies -p webserverauthentication myloadbalancer

Set the created policy to the listener by specifying the instance's port number. For example: 

    eulb-set-lb-policies-for-backend-server -i 443 -p webserverauthentication myloadbalancer

Make sure the policy is attached to the intended listener. For example: 

    eulb-describe-lbs --show-long myloadbalancer
    LOAD_BALANCER myloadbalancer
    myloadbalancer-000550595745.lb.c-04.autoqa.qa1.eucalyptus-systems.com
    {interval=30,target=TCP:8443,timeout=5,healthy-threshold=3,unhealthy-threshold=3} one \
    {protocol=HTTPS,lb-port=443,instance-protocol=HTTPS,instance-port=8443,cert-id=arn:aws:iam::000550595745:server-certificate/mycert01,\
    {ELBSecurityPolicy-2015-05}}
    {instance-port=8443,policies={webserverauthentication}}
    {ELBSecurityPolicy-2015-05,webservercert,webserverauthentication}
    {owner-alias=000936883517,group-name=euca-internal-000550595745-myloadbalancer}
    2015-10-12T20:55:52.08Z
    internet-facing

