+++
title = "Configure the Load Balancer"
weight = 60
+++


## Install and Register the Load Balancer Image
Eucalyptus provides a tool for installing and registering the Load Balancer image. Once you have run the tool, your Load Balancer will be ready to use.

Run the following commands on the machine where you installed the `eucalyptus-service-image` RPM package (it will set the `imaging.imaging_worker_emi` property to the newly created EMI of the imaging worker): 

    esi-install-image --install-default

## Verify Load Balancer Configuration
If you would like to verify that Load Balancer support is enabled you can list installed Load Balancers. The currently active Load Balancer will be listed as enabled. If no Load Balancers are listed, or none are marked as enabled, then your Load Balancer support has not been configured properly.Run the following command to list installed Load Balancer images: 

    esi-describe-images

This will produce output similar to the followin: 

    SERVICE     VERSION  ACTIVE     IMAGE      INSTANCES
        imaging       2.2      *     emi-573925e5      0
     loadbalancing    2.2      *     emi-573925e5      0
        database      2.2      *     emi-573925e5      0

You can also check the enabled Load Balancer EMI with: 

    euctl services.loadbalancing.worker.image

If you need to manually set the enabled Load Balancer EMI use: 

    euctl services.loadbalancing.worker.image=emi-12345678

