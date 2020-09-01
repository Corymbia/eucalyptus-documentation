+++
title = "Delegate Access Across Your Accounts Using Roles"
weight = 5
+++

..  _roles_tasks_cross_acct_apli_access:

A role can be used to delegate access to resources that are in different accounts that you own.Using roles to access resources across different accounts allows users to assume a role that can access all the resources in in different acccounts, rather than having users log into different accounts to achieve the same result. 

==================================================
Using Roles to Access Resources in Another Account
==================================================

The scenario described in this section outlines the procedure for a user in Account B to create a role that provides access to a particular OSGObject Storage Gateway (OSG) bucket owned by Account B, which can be assumed by user in Account A.Using `s3cmd <https://github.com/s3tools/s3cmd>`_ , list bucket that will be shared through role: 

.. code::

  # ./s3cmd/s3cmd --config=.s3cfg-acctB-user11 ls s3://mongodb-snapshots
  2014-12-01 22:34 188563920   s3://mongodb-snapshots/mongodb-backup-monday.img.xz
  2014-12-02 13:34 188564068   s3://mongodb-snapshots/mongodb-backup-tuesday.img.xz

Create Role in Account B with Trust Policy for User from Account A: 

.. code::

  # cat acctB-role-trust-acctA-policy.json
  {
    "Version": "2012-10-17",
    "Statement": [{
      "Effect": "Allow",
      "Principal": {"AWS": "arn:aws:iam::290122656840:user/user01"},
      "Action": "sts:AssumeRole"
    }]
  }
  
  # euare-rolecreate --role-name cross-bucket-access-mongodb-logs --policy-document acctB-role-trust-acctA-policy.json

Upload IAM Access Policy for Role in Account B: 

.. code::

  # cat acctB-mongodb-snapshots-bucket-access-policy.json
  {
    "Version": "2012-10-17",
    "Statement": [
      {
        "Effect": "Allow",
        "Action": "s3:ListBucket",
        "Resource": "arn:aws:s3:::mongodb-snapshots"
      },
      {
        "Effect": "Allow",
        "Action": [
          "s3:GetObject",
          "s3:PutObject",
          "s3:DeleteObject"
        ],
        "Resource": "arn:aws:s3:::mongodb-snapshots/*"
      }
    ]
  }
  
  # euare-roleuploadpolicy --role-name cross-bucket-access-mongodb-logs --policy-document acctB-mongodb-snapshots-bucket-access-policy.json --policy-name mongodb-logs-bucket-access

Upload IAM access policy to Group (e.g. Testers) associated with user in Account A to allow for Role in Account B to be assumed. For more information, go to `Amazon Web Services IAM Best Practices <http://docs.aws.amazon.com/IAM/latest/UserGuide/IAMBestPractices.html#use-groups-for-permissions>`_ . 

.. code::

  # cat acctA-assume-role-acctB-policy.json
  {
    "Statement": [
      {
        "Sid": "Stmt1417531456446",
        "Action": [
          "sts:AssumeRole"
        ],
        "Effect": "Allow",
        "Resource": "arn:aws:iam::325271821652:role/cross-bucket-access-mongodb-logs"
      }
    ]
  }
  
  # euare-groupuploadpolicy --policy-name mongodb-bucket-access-role --group-name Testers --policy-document acctA-assume-role-acctB-policy.json

The example below demonstrates how to use a python script leveraging the `boto <http://boto.readthedocs.org/en/latest/index.html>`_ library. Another way to assume this role is to run the Euca2ools command, ``euare-assumerole`` , using the AccountA/user01 credentials. For more information regarding assuming a role, see an example from the ` <../iam-guide/roles_tasks_assume_role_application.dita>`_ section. The script below performs the following actions: 

* Accesses STS to get temporary access key, secret key and token 

* List contents of bucket "mongodb-snapshots" 



.. code::

  =======================	
  #!/bin/env python
  
  import boto
  from boto.sts import STSConnection
  from boto.s3.connection import S3Connection
  from boto.s3.connection import OrdinaryCallingFormat
  
  if __name__ == "__main__":
      """
      Assuming 'cross-bucket-access-mongodb-logs' role by AccountA, User01 user
      """
      STSConnection.DefaultRegionEndpoint = "tokens.future.euca-hasp.cs.prc.eucalyptus-systems.com"
      sts_connection = STSConnection(aws_access_key_id="<AccountA User01 Access Key ID>",
      aws_secret_access_key="<AccountA User01 Secret Key>",
      is_secure=False, port="8773")
      assumedRoleObject = sts_connection.assume_role(
      role_arn="arn:aws:iam::325271821652:role/cross-bucket-access-mongodb-logs",
      role_session_name="AcctAUser01MongoDBBucketAccess")
  
      s3 = S3Connection(aws_access_key_id=assumedRoleObject.credentials.access_key,
      aws_secret_access_key=assumedRoleObject.credentials.secret_key,
      security_token=assumedRoleObject.credentials.session_token,
      host="objectstorage.future.euca-hasp.cs.prc.eucalyptus-systems.com",
      is_secure=False, port=8773, calling_format=OrdinaryCallingFormat())
  
      bucket_name = "mongodb-snapshots"
      bucket = s3.lookup(bucket_name)
      if bucket:
          print "Bucket Information [%s]:" % bucket_name
          print "------------------------------------------------------------"
          for key in bucket:
              print "\t" + key.name
      else:
          print "Bucket is not available: " + bucket_name + "\n"
  ==================

Run the script: 

.. code::

  # ./describe-bucket-script.py
  Bucket Information [mongodb-snapshots]:
  ------------------------------------------------------------
  	mongodb-backup-monday.img.xz
  	mongodb-backup-tuesday.img.xz

For information about Euca2ools IAM commands, see ` <../euca2ools-guide/eiam.dita>`_ . 