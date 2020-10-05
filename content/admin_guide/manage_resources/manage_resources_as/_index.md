+++
title = "Manage Auto Scaling Resources"
weight = 10
+++

You can list, delete, update, and suspend your Eucalyptus cloud's Autoscaling resources by passing the option with the keyword with the appropriate command.The followings are some examples you can use to act on your Auto Scaling resources.

To show all launch configurations in your cloud, run the following command: 

    euscale-describe-launch-configs --show-long verbose

To show all Auto Scaling instances in your cloud, run the following command: 

    euscale-describe-auto-scaling-groups --show-long verbose

To show all Auto Scaling instances in your cloud, run the following command: 

    euscale-describe-auto-scaling-groups --show-long verbose

To delete an Auto Scaling resource in your cloud, first get the ARN of the resource, as in this example: 

    $ euscale-describe-launch-configs --show-long verbose
    LAUNCH-CONFIG  TestLaunchConfig  emi-06663A57  m1.medium  2013-10-30T22:52:39.392Z  true
    arn:aws:autoscaling::961915002812:launchConfiguration:5ac29caf-9aad-4bdb-b228-5f
    ce841dc062:launchConfigurationName/TestLaunchConfig

Then run the following command with the ARN: 



    euscale-delete-launch-config
    arn:aws:autoscaling::961915002812:launchConfiguration:5ac29caf-9aad-4bdb-b228-5f
    ce841dc062:launchConfigurationName/TestLaunchConfig

