+++
title = "OSG Advanced Configuration"
weight = 10
+++

The following properties are for tuning the behavior of the Object Storage service and Gateways; the defaults are reasonable and changing is not necessary, but they are available for unexpected situations. 



| Property | Description | 
|  :---- |  :---- | 
| objectstorage.bucket_creation_wait_interval_seconds | The interval, in seconds, during which buckets in a 'creating' state are valid. After this interval, the operation is assumed failed. Valid values: integer > 0Default: 60 | 
| objectstorage.bucket_naming_restrictions | The S3 bucket naming restrictions to enforce. Use dns_compliant for non-US region S3 names. Use extended for US-Standard Region naming. For more information, see Bucket Restrictions and Limitations in the Amazon S3 documentation. Valid values: dns-compliant | extendedDefault: extended[]({{< relref "" >}}) | 
| objectstorage.cleanuptaskintervalseconds | The interval, in seconds, at which background cleanup tasks are run. The background cleanup tasks purge the backend of overwritten objects and clean object history. Valid values: integer > 0Default: 60 | 
| objectstorage.dogetcopyputonfail | When this property is enabled (true), the OSG attempts to perform a manual copy (performing a GET operation on the source, followed by a PUT operation on the destination) whenever the copy operation fails against the upstream provider. Because manual copies can be slow and memory-intensive, this capability is disabled (false) by default. Valid values: true | falseDefault: false | 
| objectstorage.failedputtimeouthours | The time, in hours, after which an uncommitted object upload is considered to be failed. This allows cleansing of metadata for objects that were pending upload when an OSG fails or is stopped in the middle of a user operation. This should be kept at least as long as the longest reasonable time to upload a single large object in order to prevent unintentional cleanup of uploads in-progress. The S3 maximum single upload size is 5GB. Valid values: integer > 0Default: 168 | 
| objectstorage.max_buckets_per_account | Maximum number of buckets per account. For more information, see Bucket Restrictions and Limitations in the Amazon S3 documentation. Valid values: integer > 0Default: 100 (the AWS limit)[]({{< relref "" >}}) | 
| objectstorage.max_total_reporting_capacity_gb | Total object storage capacity for objects, used solely for reporting usage percentage. Not a size restriction. No enforcement of this value. Valid values: integer > 0Default: 2147483647 (maximum value of an integer) | 
| objectstorage.queue_size | The size, in chunks, of the internal buffers that queue data for transfer to the backend on a per-request basis. A larger value will allow more buffering in the OSG when the client is uploading quickly, but the backend bandwidth is lower and cannot consume data fast enough. Too large a value may result in out-of-memory (OOM) errors if the JVM does not have sufficient heap space to handle the concurrent requests * queue_size.Valid values: integer > 0Default: 100 | 
| objectstorage.s3provider.s3usebackenddns | Use DNS virtual-hosted-style bucket names for communication to service backend. Valid values: true | falseDefault: false | 
| objectstorage.s3provider.s3usehttps | Whether or not to use HTTPS for the connections to the backend provider. If you configure this, be sure you can use the backend properly with HTTPS (certs, etc.) or the OSG will fail to connect. For RiakCS, you must configure certificates and identities to support HTTPS; it is not enabled in a default RiakCS installation.Valid values: true | falseDefault: false | 

