+++
title = "Simple Queue Service Overview"
weight = 20
+++

## Using the AWS CLI

The AWS CLI can be used to access the Simple Queue Service (SQS). Use of the Eucalyptus AWS CLI plug-in is assumed in these examples.

To list queues:

```bash
# aws sqs list-queues
QUEUEURLS	http://sqs.mycloud.example.com:8773/000575948401/queue1
QUEUEURLS	http://sqs.mycloud.example.com:8773/000575948401/sqs-1-DeadLetterQueue-N7AHZIWZEW3H5
```

Send a message:

```bash
# aws sqs send-message --queue-url http://sqs.mycloud.example.com:8773/000575948401/queue1 --message-body "TEST MESSAGE"
d41d8cd98f00b204e9800998ecf8427e	2b3ce69548da118bf617bfdd33a06108	daedefab-669b-47a4-a801-8b84e747c11c
```

Receive a messge:

```bash
# aws sqs receive-message --queue-url http://sqs.mycloud.example.com:8773/000575948401/queue1
MESSAGES	TEST MESSAGE	2b3ce69548da118bf617bfdd33a06108	d41d8cd98f00b204e9800998ecf8427e	9cc9bc8c-c201-4a27-9f7f-94924a79968a	000575948401:queue1:9cc9bc8c-c201-4a27-9f7f-94924a79968a:3
```

## Using CloudFormation

A CloudFormation template can be used to manage SQS resources. The following template is an example showing the:

* *AWS::SQS::Queue*
* *AWS::SQS::QueuePolicy*

CloudFormation resources:

```yaml
AWSTemplateFormatVersion: 2010-09-09
Description: >-
  SQS queue and queue policy template
  
Resources:

  Queue:
    Type: AWS::SQS::Queue
    Properties:
      RedrivePolicy:
        deadLetterTargetArn: !GetAtt 'DeadLetterQueue.Arn'
        maxReceiveCount: 5
      DelaySeconds: '10'
      MaximumMessageSize: '65536'
      MessageRetentionPeriod: '1209600'
      VisibilityTimeout: '20'
      ReceiveMessageWaitTimeSeconds: '5'
      QueueName: queue1

  DeadLetterQueue:
    Type: AWS::SQS::Queue

  QueuePolicy:
    Type: AWS::SQS::QueuePolicy
    Properties:
      PolicyDocument:
        Statement:
          Action: sqs:*
          Principal:
            AWS: !Ref 'AWS::AccountId'
          Effect: Allow
      Queues:
        - !Ref Queue
        - !Ref DeadLetterQueue

Outputs:

  QueueURL:
    Description: URL of the queue
    Value: !Ref 'Queue'

  QueueARN:
    Description: ARN of the queue
    Value: !GetAtt 'Queue.Arn'

  DeadLetterQueueURL:
    Description: URL of the dead letter queue
    Value: !Ref 'DeadLetterQueue'

  DeadLetterQueueARN:
    Description: ARN of the dead letter queue
    Value: !GetAtt 'DeadLetterQueue.Arn'
```

The output for the stack will show the URLs and ARNs for the created queue resources.
