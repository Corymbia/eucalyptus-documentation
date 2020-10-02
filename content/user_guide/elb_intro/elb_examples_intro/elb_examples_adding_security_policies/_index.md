+++
title = "Adding and Editing Predefined Security Policies"
weight = 10
hidden = true
+++

This topic describes how to add and edit ELB security policies.Default ELB policies are stored as JSON files in the `/etc/eucalyptus/cloud.d/elb-security-policy` directory. You can add or edit policy files here, and the changes will take effect when the CLC is restarted. 

Copy one of the ELB policy files to a new file and edit the file. You must change the `PolicyName` attribute to a new name, with the name ending in a date. For example: `ELBSecurityPolicy-2015-09` The policy file with the most recent date appended to the name will be used as the default policy when users create HTTPS/SSL listeners. The following is an example of an ELB policy file. You can modify this file and save it with a new filename in the `/etc/eucalyptus/cloud.d/elb-security-policy` directory. 
    {
        "PolicyAttributeDescriptions": [
            {
                "AttributeName": "Protocol-SSLv2",
                "AttributeValue": "false"
            },
            {
                "AttributeName": "Protocol-TLSv1",
                "AttributeValue": "true"
            },
            {
                "AttributeName": "Protocol-SSLv3",
                "AttributeValue": "false"
            },
            {
                "AttributeName": "Protocol-TLSv1.1",
                "AttributeValue": "true"
            },
            {
                "AttributeName": "Protocol-TLSv1.2",
                "AttributeValue": "true"
            },
            {
                "AttributeName": "Server-Defined-Cipher-Order",
                "AttributeValue": "true"
            },
            {
                "AttributeName": "ECDHE-ECDSA-AES128-GCM-SHA256",
                "AttributeValue": "true"
            },
            {
                "AttributeName": "ECDHE-RSA-AES128-GCM-SHA256",
                "AttributeValue": "true"
            },
            {
                "AttributeName": "ECDHE-ECDSA-AES128-SHA256",
                "AttributeValue": "true"
            },
            {
                "AttributeName": "ECDHE-RSA-AES128-SHA256",
                "AttributeValue": "true"
            },
            {
                "AttributeName": "ECDHE-ECDSA-AES128-SHA",
                "AttributeValue": "true"
            },
            {
                "AttributeName": "ECDHE-RSA-AES128-SHA",
                "AttributeValue": "true"
            },
            {
                "AttributeName": "DHE-RSA-AES128-SHA",
                "AttributeValue": "false"
            },
            {
                "AttributeName": "ECDHE-ECDSA-AES256-GCM-SHA384",
                "AttributeValue": "true"
            },
            {
                "AttributeName": "ECDHE-RSA-AES256-GCM-SHA384",
                "AttributeValue": "true"
            },
            {
                "AttributeName": "ECDHE-ECDSA-AES256-SHA384",
                "AttributeValue": "true"
            },
            {
                "AttributeName": "ECDHE-RSA-AES256-SHA384",
                "AttributeValue": "true"
            },
            {
                "AttributeName": "ECDHE-RSA-AES256-SHA",
                "AttributeValue": "true"
            },
            {
                "AttributeName": "ECDHE-ECDSA-AES256-SHA",
                "AttributeValue": "true"
            },
            {
                "AttributeName": "AES128-GCM-SHA256",
                "AttributeValue": "true"
            },
            {
                "AttributeName": "AES128-SHA256",
                "AttributeValue": "true"
            },
            {
                "AttributeName": "AES128-SHA",
                "AttributeValue": "true"
            },
            {
                "AttributeName": "AES256-GCM-SHA384",
                "AttributeValue": "true"
            },
            {
                "AttributeName": "AES256-SHA256",
                "AttributeValue": "true"
            },
            {
                "AttributeName": "AES256-SHA",
                "AttributeValue": "true"
            },
            {
                "AttributeName": "DHE-DSS-AES128-SHA",
                "AttributeValue": "false"
            },
            {
                "AttributeName": "CAMELLIA128-SHA",
                "AttributeValue": "false"
            },
            {
                "AttributeName": "EDH-RSA-DES-CBC3-SHA",
                "AttributeValue": "false"
            },
            {
                "AttributeName": "DES-CBC3-SHA",
                "AttributeValue": "true"
            },
            {
                "AttributeName": "ECDHE-RSA-RC4-SHA",
                "AttributeValue": "false"
            },
            {
                "AttributeName": "RC4-SHA",
                "AttributeValue": "false"
            },
            {
                "AttributeName": "ECDHE-ECDSA-RC4-SHA",
                "AttributeValue": "false"
            },
            {
                "AttributeName": "DHE-DSS-AES256-GCM-SHA384",
                "AttributeValue": "false"
            },
            {
                "AttributeName": "DHE-RSA-AES256-GCM-SHA384",
                "AttributeValue": "false"
            },
            {
                "AttributeName": "DHE-RSA-AES256-SHA256",
                "AttributeValue": "false"
            },
            {
                "AttributeName": "DHE-DSS-AES256-SHA256",
                "AttributeValue": "false"
            },
            {
                "AttributeName": "DHE-RSA-AES256-SHA",
                "AttributeValue": "false"
            },
            {
                "AttributeName": "DHE-DSS-AES256-SHA",
                "AttributeValue": "false"
            },
            {
                "AttributeName": "DHE-RSA-CAMELLIA256-SHA",
                "AttributeValue": "false"
            },
            {
                "AttributeName": "DHE-DSS-CAMELLIA256-SHA",
                "AttributeValue": "false"
            },
            {
                "AttributeName": "CAMELLIA256-SHA",
                "AttributeValue": "false"
            },
            {
                "AttributeName": "EDH-DSS-DES-CBC3-SHA",
                "AttributeValue": "false"
            },
            {
                "AttributeName": "DHE-DSS-AES128-GCM-SHA256",
                "AttributeValue": "false"
            },
            {
                "AttributeName": "DHE-RSA-AES128-GCM-SHA256",
                "AttributeValue": "false"
            },
            {
                "AttributeName": "DHE-RSA-AES128-SHA256",
                "AttributeValue": "false"
            },
            {
                "AttributeName": "DHE-DSS-AES128-SHA256",
                "AttributeValue": "false"
            },
            {
                "AttributeName": "DHE-RSA-CAMELLIA128-SHA",
                "AttributeValue": "false"
            },
            {
                "AttributeName": "DHE-DSS-CAMELLIA128-SHA",
                "AttributeValue": "false"
            },
            {
                "AttributeName": "ADH-AES128-GCM-SHA256",
                "AttributeValue": "false"
            },
            {
                "AttributeName": "ADH-AES128-SHA",
                "AttributeValue": "false"
            },
            {
                "AttributeName": "ADH-AES128-SHA256",
                "AttributeValue": "false"
            },
            {
                "AttributeName": "ADH-AES256-GCM-SHA384",
                "AttributeValue": "false"
            },
            {
                "AttributeName": "ADH-AES256-SHA",
                "AttributeValue": "false"
            },
            {
                "AttributeName": "ADH-AES256-SHA256",
                "AttributeValue": "false"
            },
            {
                "AttributeName": "ADH-CAMELLIA128-SHA",
                "AttributeValue": "false"
            },
            {
                "AttributeName": "ADH-CAMELLIA256-SHA",
                "AttributeValue": "false"
            },
            {
                "AttributeName": "ADH-DES-CBC3-SHA",
                "AttributeValue": "false"
            },
            {
                "AttributeName": "ADH-DES-CBC-SHA",
                "AttributeValue": "false"
            },
            {
                "AttributeName": "ADH-RC4-MD5",
                "AttributeValue": "false"
            },
            {
                "AttributeName": "ADH-SEED-SHA",
                "AttributeValue": "false"
            },
            {
                "AttributeName": "DES-CBC-SHA",
                "AttributeValue": "false"
            },
            {
                "AttributeName": "DHE-DSS-SEED-SHA",
                "AttributeValue": "false"
            },
            {
                "AttributeName": "DHE-RSA-SEED-SHA",
                "AttributeValue": "false"
            },
            {
                "AttributeName": "EDH-DSS-DES-CBC-SHA",
                "AttributeValue": "false"
            },
            {
                "AttributeName": "EDH-RSA-DES-CBC-SHA",
                "AttributeValue": "false"
            },
            {
                "AttributeName": "IDEA-CBC-SHA",
                "AttributeValue": "false"
            },
            {
                "AttributeName": "RC4-MD5",
                "AttributeValue": "false"
            },
            {
                "AttributeName": "SEED-SHA",
                "AttributeValue": "false"
            },
            {
                "AttributeName": "DES-CBC3-MD5",
                "AttributeValue": "false"
            },
            {
                "AttributeName": "DES-CBC-MD5",
                "AttributeValue": "false"
            },
            {
                "AttributeName": "RC2-CBC-MD5",
                "AttributeValue": "false"
            },
            {
                "AttributeName": "PSK-AES256-CBC-SHA",
                "AttributeValue": "false"
            },
            {
                "AttributeName": "PSK-3DES-EDE-CBC-SHA",
                "AttributeValue": "false"
            },
            {
                "AttributeName": "KRB5-DES-CBC3-SHA",
                "AttributeValue": "false"
            },
            {
                "AttributeName": "KRB5-DES-CBC3-MD5",
                "AttributeValue": "false"
            },
            {
                "AttributeName": "PSK-AES128-CBC-SHA",
                "AttributeValue": "false"
            },
            {
                "AttributeName": "PSK-RC4-SHA",
                "AttributeValue": "false"
            },
            {
                "AttributeName": "KRB5-RC4-SHA",
                "AttributeValue": "false"
            },
            {
                "AttributeName": "KRB5-RC4-MD5",
                "AttributeValue": "false"
            },
            {
                "AttributeName": "KRB5-DES-CBC-SHA",
                "AttributeValue": "false"
            },
            {
                "AttributeName": "KRB5-DES-CBC-MD5",
                "AttributeValue": "false"
            },
            {
                "AttributeName": "EXP-EDH-RSA-DES-CBC-SHA",
                "AttributeValue": "false"
            },
            {
                "AttributeName": "EXP-EDH-DSS-DES-CBC-SHA",
                "AttributeValue": "false"
            },
            {
                "AttributeName": "EXP-ADH-DES-CBC-SHA",
                "AttributeValue": "false"
            },
            {
                "AttributeName": "EXP-DES-CBC-SHA",
                "AttributeValue": "false"
            },
            {
                "AttributeName": "EXP-RC2-CBC-MD5",
                "AttributeValue": "false"
            },
            {
                "AttributeName": "EXP-KRB5-RC2-CBC-SHA",
                "AttributeValue": "false"
            },
            {
                "AttributeName": "EXP-KRB5-DES-CBC-SHA",
                "AttributeValue": "false"
            },
            {
                "AttributeName": "EXP-KRB5-RC2-CBC-MD5",
                "AttributeValue": "false"
            },
            {
                "AttributeName": "EXP-KRB5-DES-CBC-MD5",
                "AttributeValue": "false"
            },
            {
                "AttributeName": "EXP-ADH-RC4-MD5",
                "AttributeValue": "false"
            },
            {
                "AttributeName": "EXP-RC4-MD5",
                "AttributeValue": "false"
            },
            {
                "AttributeName": "EXP-KRB5-RC4-SHA",
                "AttributeValue": "false"
            },
            {
                "AttributeName": "EXP-KRB5-RC4-MD5",
                "AttributeValue": "false"
            }
        ],
        "PolicyName": "ELBSecurityPolicy-2015-05",
        "PolicyTypeName": "SSLNegotiationPolicyType"
    }

Using a text editor, change the `PolicyName` attribute. For example: `"PolicyName": "ELBSecurityPolicy-2015-05"` Once you've edited and saved the JSON file, restart the CLC. Once the CLC has restarted, use the `eulb-describe-lb-policies` command to verify that your new policy is listed. For example: 


    POLICY	ELBSample-AppCookieStickinessPolicy	AppCookieStickinessPolicyType
    POLICY	ELBSample-LBCookieStickinessPolicy	LBCookieStickinessPolicyType
    POLICY	ELBSecurityPolicy-2014-10	SSLNegotiationPolicyType
    POLICY	ELBSecurityPolicy-2015-02	SSLNegotiationPolicyType
    POLICY	ELBSecurityPolicy-2011-08	SSLNegotiationPolicyType
    POLICY	ELBSecurityPolicy-2015-05	SSLNegotiationPolicyType
    POLICY	ELBSecurityPolicy-2014-01	SSLNegotiationPolicyType
    POLICY	MyNewELBSecurityPolicy-2015-09	SSLNegotiationPolicyType

You can now use your new security policy using the `eulb-create-lb-policy` command. For more information, see [](elb_examples_ssl_negotiation.dita) . 