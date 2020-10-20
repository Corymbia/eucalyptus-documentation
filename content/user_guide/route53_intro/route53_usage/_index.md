+++
title = "Route53 Usage"
weight = 20
+++

This section describes some options for access to the Route53 service and shows some example usage.

## Using the AWS CLI

The AWS CLI can be used to access Route53. Use of the Eucalyptus AWS CLI plug-in is assumed in these examples.

To list hosted zones:

```bash
# aws route53 list-hosted-zones
HOSTEDZONES	e001e659-32ac-4fd5-b45a-f7e6d6420f9b	/hostedzone/ZAAW4ODX2K7WOL	subdomain.example.com.	3
CONFIG	Private zone for subdomain.example.com in vpc-837bc081de161f8c0	True
```

To list resource records for a hosted zone:

```bash
# aws route53 list-resource-record-sets --hosted-zone-id ZAAW4ODX2K7WOL
RESOURCERECORDSETS	alias.subdomain.example.com.	0	A
RESOURCERECORDSETS	cname.subdomain.example.com.	300	CNAME
RESOURCERECORDS	name.subdomain.example.com
RESOURCERECORDSETS	name.subdomain.example.com.	300	A
RESOURCERECORDS	10.20.30.43
```

The AWS CLI can be used to create and delete hosted zones and to change resource record sets.

## Using CloudFormation

A CloudFormation template can be used to manage Route53 resources. The following template is an example showing the:

* *AWS::Route53::HostedZone*
* *AWS::Route53::RecordSet*
* *AWS::Route53::RecordSetGroup*

CloudFormation resources:

```yaml
AWSTemplateFormatVersion: 2010-09-09
Description: >-
  Route53 private HostedZone

Parameters:

  Vpc:
    Description: The VPC to create the Zone for
    Type: String

  Zone:
    Description: The zone to create
    Type: String
    Default: example.com

Resources:

  MyHostedZone:
    Type: AWS::Route53::HostedZone
    Properties:
      Name: !Ref Zone
      HostedZoneConfig:
        Comment: !Sub "Private zone for ${Zone} in ${Vpc}"
      VPCs:
        - VPCId: !Ref Vpc
          VPCRegion: !Ref AWS::Region
      HostedZoneTags:
        - Key: example-tag
          Value: !Ref Zone

  MyRecordSet:
    Type: AWS::Route53::RecordSet
    DependsOn: MyHostedZone
    Properties:
      HostedZoneName: !Ref Zone
      Name: !Sub "name.${Zone}"
      ResourceRecords:
        - "10.20.30.43"
      TTL: 300
      Type: A

  MyRecordSetGroup:
    Type: AWS::Route53::RecordSetGroup
    DependsOn: MyHostedZone
    Properties:
      HostedZoneName: !Ref Zone
      RecordSets:
        - Name: !Sub "cname.${Zone}"
          ResourceRecords:
          - !Sub "name.${Zone}"
          TTL: 300
          Type: CNAME
        - Name: !Sub "alias.${Zone}"
          Type: A
          AliasTarget:
            DNSName: !Sub "name.${Zone}"
            EvaluateTargetHealth: no
            HostedZoneId: !Ref MyHostedZone

Outputs:

  HostedZoneId:
    Description: The identifier for the private hosted zone
    Value: !Ref MyHostedZone
```

The output for the stack will show the identifier for the hosted zone.

