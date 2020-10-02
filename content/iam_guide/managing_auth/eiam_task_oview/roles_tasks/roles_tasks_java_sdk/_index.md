+++
title = "Use a Role with an Instance Application"
weight = 10
+++

You can use the AWS Java SDK to programmatically perform IAM role-related operations in your Eucalyptus cloud. This example shows how to use the AWS SDK to retrieve the credentials for the IAM role associated with the Eucalyptus instance.The following program lists the contents of the bucket "my-test-bucket" using the credentials stored in the Java system properties: 
    import com.amazonaws.auth.*;
    import com.amazonaws.AmazonClientException;
    import com.amazonaws.AmazonServiceException;
    import com.amazonaws.auth.AWSCredentialsProvider;
    import com.amazonaws.auth.ClasspathPropertiesFileCredentialsProvider;
    import com.amazonaws.services.ec2.AmazonEC2;
    import com.amazonaws.services.ec2.AmazonEC2Client;
    import com.amazonaws.services.s3.*;
    import com.amazonaws.services.s3.model.*;
    
    public class MyTestApp {
    
        static AmazonEC2 ec2;
        static AmazonS3 s3;
    
        private static void init() throws Exception {
    
            AWSCredentialsProvider credentials = new ClasspathPropertiesFileCredentialsProvider();
     
            s3 = new AmazonS3Client(credentials);
            s3.setEndpoint("http://128.0.0.1:8773/services/Walrus");
        }
    
    
        public static void main(String[] args) throws Exception {
    
            init();
    
            try {
               
                String bucketName = "my-test-bucket";           
                System.out.println("Listing bucket " + bucketName + ":");
                ListObjectsRequest listObjectsRequest = new ListObjectsRequest(bucketName, "", "", "", 200);
                ObjectListing bucketList;
                do {
                    bucketList = s3.listObjects(listObjectsRequest);
                    for (S3ObjectSummary objectInfo :
                            bucketList.getObjectSummaries()) {
                        System.out.println(" - " + objectInfo.getKey() + "  " +
                                "(size = " + objectInfo.getSize() +
                                ")");
                    }
                    listObjectsRequest.setMarker(bucketList.getNextMarker());
                } while (bucketList.isTruncated());
    
            } catch (AmazonServiceException eucaServiceException ) {
                System.out.println("Exception: " + eucaServiceException.getMessage());
                System.out.println("Status Code: " + eucaServiceException.getStatusCode());
                System.out.println("Error Code: " + eucaServiceException.getErrorCode());
                System.out.println("Request ID: " + eucaServiceException.getRequestId());
            } catch (AmazonClientException eucaClientException) {
                System.out.println("Error Message: " + eucaClientException.getMessage());
            }
            System.out.println("===== FINISHED =====");
        }
    
    }                    

This application produces output similar to the following: 


    Listing bucket my-test-bucket:
     - precise-server-cloudimg-amd64-vmlinuz-virtual.manifest.xml  (size = 3553)
     - precise-server-cloudimg-amd64-vmlinuz-virtual.part.0  (size = 4904032)
     - precise-server-cloudimg-amd64.img.manifest.xml  (size = 7014)
     - precise-server-cloudimg-amd64.img.part.0  (size = 10485760)
     - precise-server-cloudimg-amd64.img.part.1  (size = 10485760)
     - precise-server-cloudimg-amd64.img.part.10  (size = 10485760)
     - precise-server-cloudimg-amd64.img.part.11  (size = 10485760)
     - precise-server-cloudimg-amd64.img.part.12  (size = 10485760)
     - precise-server-cloudimg-amd64.img.part.13  (size = 10485760)
     - precise-server-cloudimg-amd64.img.part.14  (size = 10485760)
     - precise-server-cloudimg-amd64.img.part.15  (size = 10485760)
     - precise-server-cloudimg-amd64.img.part.16  (size = 10485760)
     - precise-server-cloudimg-amd64.img.part.17  (size = 10485760)
     - precise-server-cloudimg-amd64.img.part.18  (size = 10485760)
     - precise-server-cloudimg-amd64.img.part.19  (size = 10485760)
     - precise-server-cloudimg-amd64.img.part.2  (size = 10485760)
     - precise-server-cloudimg-amd64.img.part.20  (size = 10485760)
     - precise-server-cloudimg-amd64.img.part.21  (size = 10485760)
     - precise-server-cloudimg-amd64.img.part.22  (size = 2570400)
     - precise-server-cloudimg-amd64.img.part.3  (size = 10485760)
     - precise-server-cloudimg-amd64.img.part.4  (size = 10485760)
     - precise-server-cloudimg-amd64.img.part.5  (size = 10485760)
     - precise-server-cloudimg-amd64.img.part.6  (size = 10485760)
     - precise-server-cloudimg-amd64.img.part.7  (size = 10485760)
     - precise-server-cloudimg-amd64.img.part.8  (size = 10485760)
     - precise-server-cloudimg-amd64.img.part.9  (size = 10485760)
    ===== FINISHED =====

The problem with this approach is that the credentials are hardcoded into the application - this makes them less secure, and makes the application more difficult to maintain. Using IAM roles is a more secure and easier way to manage credentials for applications that run on Eucalyptus cloud instances. 

Create a role with a policy that allows an instance to list the contents of a specific bucket, and then launch an instance with that role (for an example, see [Launch an Instance with a Role](roles_tasks_create_role_application.dita) . An example policy that allows listing of a specific bucket will look similar to the following: 
    {
      "Statement": [
        {
          "Action": [
            "s3:ListBucket"
          ],
          "Effect": "Allow",
          "Resource": "arn:aws:s3:::my-test-bucket"
        }
      ]
    }             

The following line of code retrieves the credentials that are stored in the application's credentials profile: `AWSCredentialsProvider credentials = new ClasspathPropertiesFileCredentialsProvider();` To use the role-based credentials associated with the instance, replace that line of code with the following: `AWSCredentialsProvider credentials = new InstanceProfileCredentialsProvider();` The program now looks like this: 


    import com.amazonaws.auth.*;
    import com.amazonaws.AmazonClientException;
    import com.amazonaws.AmazonServiceException;
    import com.amazonaws.auth.AWSCredentialsProvider;
    import com.amazonaws.auth.ClasspathPropertiesFileCredentialsProvider;
    import com.amazonaws.services.ec2.AmazonEC2;
    import com.amazonaws.services.ec2.AmazonEC2Client;
    import com.amazonaws.services.s3.*;
    import com.amazonaws.services.s3.model.*;
    
    public class MyTestApp {
    
        static AmazonEC2 ec2;
        static AmazonS3 s3;
    
        private static void init() throws Exception {
    
            AWSCredentialsProvider credentials = new InstanceProfileCredentialsProvider();
     
            s3 = new AmazonS3Client(credentials);
            s3.setEndpoint("http://128.0.0.1:8773/services/Walrus");
        }
    
    
        public static void main(String[] args) throws Exception {
    
            init();
    
            try {
               
                String bucketName = "my-test-bucket";
               
                System.out.println("Listing bucket " + bucketName + ":");
                ListObjectsRequest listObjectsRequest = new ListObjectsRequest(bucketName, "", "", "", 200);
                ObjectListing bucketList;
                do {
                    bucketList = s3.listObjects(listObjectsRequest);
                    for (S3ObjectSummary objectInfo :
                            bucketList.getObjectSummaries()) {
                        System.out.println(" - " + objectInfo.getKey() + "  " +
                                "(size = " + objectInfo.getSize() +
                                ")");
                    }
                    listObjectsRequest.setMarker(bucketList.getNextMarker());
                } while (bucketList.isTruncated());
    
            } catch (AmazonServiceException eucaServiceException ) {
                System.out.println("Exception: " + eucaServiceException.getMessage());
                System.out.println("Status Code: " + eucaServiceException.getStatusCode());
                System.out.println("Error Code: " + eucaServiceException.getErrorCode());
                System.out.println("Request ID: " + eucaServiceException.getRequestId());
            } catch (AmazonClientException eucaClientException) {
                System.out.println("Error Message: " + eucaClientException.getMessage());
            }
            System.out.println("===== FINISHED =====");
        }
    
    }

NOTE: Running this code outside of an instance will result in the following error message: 


    Listing bucket my-test-bucket:
    Error Message: Unable to load credentials from Amazon EC2 metadata service



When the application is running on an instance that was launched with the role you created, the credentials for the role assigned to the instance will be retrieved from the Instance Metadata Service. 