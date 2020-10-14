+++
title = "Updating the SSL Negotiation Configuration"
weight = 80
+++

Eucalyptus Elastic Load Balancing (ELB) uses SSL negotiation configurations to determine how SSL connections to your load balancer behave. This topic shows how to update an existing load balancer with an SSL negotiation configuration. 

Get a list of predefined security policies using the `eulb-describe-lb-policies` command: `eulb-describe-lb-policies` This produces output similar to the following: 

    POLICY	ELBSample-AppCookieStickinessPolicy	AppCookieStickinessPolicyType
    POLICY	ELBSample-LBCookieStickinessPolicy	LBCookieStickinessPolicyType
    POLICY	ELBSecurityPolicy-2014-10	SSLNegotiationPolicyType
    POLICY	ELBSecurityPolicy-2015-02	SSLNegotiationPolicyType
    POLICY	ELBSecurityPolicy-2011-08	SSLNegotiationPolicyType
    POLICY	ELBSecurityPolicy-2015-05	SSLNegotiationPolicyType
    POLICY	ELBSecurityPolicy-2014-01	SSLNegotiationPolicyType

Use the `eulb-create-lb-policy` command to update the SSL negotiation configuration to use one of the predefined security policies. For example: `eulb-create-lb-policy --policy-name mypredefinedsslpolicy --policy-type SSLNegotiationPolicyType --attributes "Reference-Security-Policy=ELBSecurityPolicy-2011-08" myloadbalancer` Use the `eulb-describe-lbs` command to verify the update. For example: `eulb-describe-lbs myloadbalancer` 
