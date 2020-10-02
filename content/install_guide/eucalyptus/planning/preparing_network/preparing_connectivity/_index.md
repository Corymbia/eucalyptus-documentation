+++
title = "Verify Connectivity"
weight = 10
hidden = true
+++


{{% notice note %}}
Any firewall running on the CC must be compatible with the dynamic changes performed by when working with security groups. will flush the 'filter' and 'nat' tables upon boot. 
{{% /notice %}}
Verify component connectivity by performing the following checks on the machines that will be running the listed Eucalyptus components. 

Verify connection from an end-user to the CLC on TCP port 8773 Verify connection from an end-user to Walrus on TCP port 8773 Verify connection from the CLC, SC, and NC to SC on TCP port 8773 Verify connection from the CLC, SC, and NC to Walrus on TCP port 8773 Verify connection from Walrus and SC to CLC on TCP port 8777 Verify connection from CLC to CC on TCP port 8774 Verify connection from CC to NC on TCP port 8775 Verify connection from NC to Walrus on TCP port 8773. Or, you can verify the connection from the CC to Walrus on port TCP 8773, and from an NC to the CC on TCP port 8776 Verify connection from public IP addresses of Eucalyptus instances (metadata) and CC to CLC on TCP port 8773 Verify TCP connectivity between CLC, Walrus, and SC on TCP port 8779 (or the first available port in range 8779-8849)  Verify connection between CLC, Walrus, and SC on UDP port 7500 Verify multicast connectivity for IP address 239.193.7.3 between CLC and UFS, OSG, Walrus, and SC on UDP port 8773 If DNS is enabled, verify connection from an end-user and instance IPs to DNS ports If you use tgt (iSCSI open source target) for EBS in DAS or Overlay modes, verify connection from NC to SC on TCP port 3260 