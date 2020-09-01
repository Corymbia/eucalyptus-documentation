+++
title = "CloudFormation Run Options"
weight = 5
+++

..  _cf_tools:

You can run CloudFormation using Euca2ools, the AWS SDK for Java, the AWS command line interface, and Boto.

=========
Euca2ools
=========

For information about Euca2ools CloudFormation commands, see ` <../euca2ools-guide/euform.dita>`_ . 



================
AWS SDK for Java
================

The AWS SDK has data types and command structures that are generally a one-to-one match to what is defined in the AWS API documentation. For more information about the SDK API, go to the `AWS SDK for Java API Reference <http://docs.aws.amazon.com/AWSJavaSDK/latest/javadoc/index.html>`_ . 

The following is an example of a describe stacks call. 



.. code::

  import com.amazonaws.services.cloudformation.AmazonCloudFormationClient;
  import com.amazonaws.services.cloudformation.model.DescribeStacksRequest;
  import com.amazonaws.services.cloudformation.model.DescribeStacksResult;
  import com.amazonaws.services.cloudformation.model.Output;
  import com.amazonaws.services.cloudformation.model.Parameter;
  import com.amazonaws.services.cloudformation.model.Stack;
  import com.amazonaws.services.cloudformation.model.Tag;
  
  public class DescribeStacksTest  {
    private static final String AWS_ACCESS_KEY = …; // Don’t really hard-code creds
    private static final String AWS_SECRET_KEY = …; // Don’t really hard-code creds
  
    private static final BasicAWSCredentials CREDS = new BasicAWSCredentials(
    	ACCESS_KEY, SECRET_KEY);
    private static final String HOST = "10.111.1.134:8773";
  
    private static final AmazonCloudFormationClient CLOUDFORMATION_CLIENT() {
      AmazonCloudFormationClient cf = new AmazonCloudFormationClient(CREDS);
      cf.setEndpoint("http://" + HOST + "/services/CloudFormation/");
      return cf;
    }
    public static void main(String[] args) {
      AmazonCloudFormationClient cloudFormation = CLOUDFORMATION_CLIENT();
      DescribeStacksRequest describeStacksRequest = new DescribeStacksRequest();
      describeStacksRequest = new DescribeStacksRequest();
      describeStacksRequest.setStackName("MyStack");
      DescribeStacksResult describeStacksResult =
        cloudFormation.describeStacks(describeStacksRequest);
      printStackResult(describeStacksResult);
    }
  
    private static void printStackResult(DescribeStacksResult describeStacksResult) {
      System.out.println("describeStacksResult.getNextToken()=" +
        describeStacksResult.getNextToken());
      for (Stack stack:describeStacksResult.getStacks()) {
        System.out.println("stack.getDescription()="+stack.getDescription());
        for (String capability: stack.getCapabilities()) {
          System.out.println("capability="+capability);
        }
        System.out.println("stack.getCreationTime()="+stack.getCreationTime());
        System.out.println("stack.getDescription()="+stack.getDescription());
        System.out.println("stack.getDisableRollback()="+stack.getDisableRollback());
        System.out.println("stack.getLastUpdatedTime()="+stack.getLastUpdatedTime());
        for (String capability: stack.getCapabilities()) {
          System.out.println("capability="+capability);
        }
        for (String notificationARN: stack.getNotificationARNs()) {
          System.out.println("notificationARN="+notificationARN);
        }
        for (Output output: stack.getOutputs()) {
          System.out.println("output.getDescription()="+output.getDescription());
          System.out.println("output.getOutputKey()="+output.getOutputKey());
          System.out.println("output.getOutputValue()="+output.getOutputValue());
    	}
       for (Parameter parameter: stack.getParameters()) {
         System.out.println("parameter.getParameterKey()="+parameter.getParameterKey());
         System.out.println("parameter.getParameterValue()="+parameter.getParameterValue());
    	}
       System.out.println("stack.getStackId()="+stack.getStackId());
       System.out.println("stack.getStackName()="+stack.getStackName());
       System.out.println("stack.getStackStatus()="+stack.getStackStatus());
       System.out.println("stack.getStackStatusReason()="+stack.getStackStatusReason());
       for (Tag tag: stack.getTags()) {
         System.out.println("tag.getKey()="+tag.getKey());
         System.out.println("tag.getValue()="+tag.getValue());
       }	
       System.out.println("stack.getTimeoutInMinutes()="+stack.getTimeoutInMinutes());
     }
   }
  }

Eucalyptus returns all of the fields, and the stack name is passed in to the call. 

For more information about the AWS SDK for Java, go to `http://aws.amazon.com/sdkforjava/ <http://aws.amazon.com/sdkforjava/>`_ . 



==========================
AWS Command Line Interface
==========================

You can use the AWS command line interface (CLI) with Eucalyptus CloudFormation. For example, the following command describes a stack: 



.. code::

  aws --endpoint http://10.111.1.134:8773/services/CloudFormation cloudformation describe-stacks

Credential information is either also passed using flags or stored in a file referenced by the ``AWS_CONFIG_FILE`` environment variable. Results from the previous command are in JSON: 



.. code::

  {
  	"Stacks": [
      	{
          	"StackId": "arn:aws:cloudformation::299958418681:stack/MyStack/c70b9e4e-fcd5-47e6-b1ae-68cdb8f9f22c",
          	"LastUpdatedTime": "2014-05-30T05:19:44.085Z",
          	"Parameters": [
              	{
                  	"ParameterValue": "emi-db0b2276",
                  	"ParameterKey": "MyImageId"
              	}
          	],
          	"Tags": [],
          	"Outputs": [],
          	"StackStatusReason": "Complete!",
          	"CreationTime": "2014-05-30T05:19:22.412Z",
          	"Capabilities": [],
          	"StackName": "MyStack",
          	"NotificationARNs": [],
          	"StackStatus": "CREATE_COMPLETE",
          	"DisableRollback": false
      	}
  	]
  }

For more information about the AWS CLI, go to `http://docs.aws.amazon.com/cli/latest/reference/cloudformation/index.html <http://docs.aws.amazon.com/cli/latest/reference/cloudformation/index.html>`_ . 



====
Boto
====

Boto is a Python API that calls the AWS web service API, and is well documented. The following snippet accesses the base CloudFormation "cf" object: 



.. code::

  import boto
  from boto.regioninfo import RegionInfo
  region = RegionInfo()
  region.endpoint = "10.111.1.134"
  region.name = "eucalyptus"
  cfn = boto.connect_cloudformation(region=region, port=8773, path="/services/CloudFormation", is_secure=False)

For more information about Boto, go to `https://github.com/boto/boto <https://github.com/boto/boto>`_ . 

