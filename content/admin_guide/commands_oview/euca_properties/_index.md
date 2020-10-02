+++
title = "Eucalyptus Configuration Variables"
weight = 10
hidden = true
+++

Eucalyptus exposes a number of variables that can be configured using the command. This topic explains what types of variables Eucalyptus uses, and lists the most common configurable variables.
## Eucalyptus Variable Types
Eucalyptus uses two types of variables: ones that can be changed (as configuration options), and ones that cannot be changed (they are displayed as variables, but configured by modifying the `eucalyptus.conf` file on the CC). 


{{% notice note %}}
Once a cloud is in use and has started operating based on these variables, it is not safe to change them at runtime. 
{{% /notice %}}

## Eucalyptus Variables
The following table contains a list of common Eucalyptus cloud variables. 



| Variable | Description | 
|  :---- |  :---- | 
| authentication.access_keys_limit | Limit for access keys per user | 
| authentication.authorization_cache | Authorization cache configuration, for credentials and authorization metadata | 
| authentication.authorization_expiry | Default expiry for cached authorization metadata | 
| authentication.authorization_reuse_expiry | Default expiry for re-use of cached authorization metadata on failure | 
| authentication.credential_download_generate_certificate | Strategy for generation of certificates on credential download (Never | Absent | Limited) | 
| authentication.credential_download_host_match | CIDR to match against for host address selection | 
| authentication.credential_download_port | Port to use in service URLs when 'bootstrap.webservices.port' is not appropriate. | 
| authentication.default_password_expiry | Default password expiry time | 
| authentication.max_policy_size | Maximum size for an IAM policy (bytes) | 
| authentication.signing_certificates_limit | Limit for signing certificates per user | 
| authentication.system_account_quota_enabled | Process quotas for system accounts | 
| autoscaling.activityexpiry | Expiry age for scaling activities. Older activities are deleted. | 
| autoscaling.activityinitialbackoff | Initial back-off period for failing activities. | 
| autoscaling.activitymaxbackoff | Maximum back-off period for failing activities. | 
| autoscaling.activitytimeout | Timeout for a scaling activity. | 
| autoscaling.maxlaunchincrement | Maximum instances to launch at one time. | 
| autoscaling.maxregistrationretries | Number of times to attempt load balancer registration for each instance. | 
| autoscaling.pendinginstancetimeout | Timeout for a pending instance. | 
| autoscaling.suspendedprocesses | Globally suspend scaling processes; a comma-delimited list of processes (Launch,Terminate,HealthCheck, ReplaceUnhealthy,AZRebalance, AlarmNotification,ScheduledActions, AddToLoadBalancer). Default is empty, meaning the processes are not suspended. | 
| autoscaling.suspendedtasks | Suspended scaling tasks. | 
| autoscaling.suspensionlaunchattemptsthreshold | Minimum launch attempts for administrative suspension of scaling activities for a group. | 
| autoscaling.suspensiontimeout | Timeout for administrative suspension of scaling activities for a group. | 
| autoscaling.untrackedinstancetimeout | Timeout for termination of untracked auto scaling instances. | 
| autoscaling.zonefailurethreshold | Time after which an unavailable zone should be treated as failed | 
| bootstrap.async.future_listener_debug_limit_secs | Number of seconds a future listener can execute before a debug message is logged. | 
| bootstrap.async.future_listener_error_limit_secs | Number of seconds a future listener can execute before an error message is logged. | 
| bootstrap.async.future_listener_get_retries | Total number of seconds a future listener's executor waits to get(). | 
| bootstrap.async.future_listener_get_timeout | Number of seconds a future listener's executor waits to get() per call. | 
| bootstrap.async.future_listener_info_limit_secs | Number of seconds a future listener can execute before an info message is logged. | 
| bootstrap.hosts.state_initialize_timeout | Timeout for state initialization (in msec). | 
| bootstrap.hosts.state_transfer_timeout | Timeout for state transfers (in msec). | 
| bootstrap.notifications.batch_delay_seconds | Interval (in seconds) during which a notification will be delayed to allow for batching events for delivery. | 
| bootstrap.notifications.digest | Send a system state digest periodically. | 
| bootstrap.notifications.digest_frequency_hours | Period (in hours) with which a system state digest will be delivered. | 
| bootstrap.notifications.digest_only_on_errors | If sending system state digests is set to true, then only send the digest when the system has failures to report. | 
| bootstrap.notifications.digest_frequency_hours | Period (in hours) with which a system state digest will be delivered. | 
| bootstrap.notifications.digest_only_on_errors | If sending system state digests is set to true, then only send the digest when the system has failures to report. | 
| bootstrap.notifications.email_from | From email address used for notification delivery. | 
| bootstrap.notifications.email_from_name | From email name used for notification delivery. | 
| bootstrap.notifications.email_from_name | From email name used for notification delivery. | 
| bootstrap.notifications.email_subject_prefix | Email subject used for notification delivery. | 
| bootstrap.notifications.email_to | Email address where notifications are to be delivered. | 
| bootstrap.notifications.include_fault_stack | Period (in hours) with which a system state digest will be delivered. | 
| bootstrap.notifications.email.email_smtp_host | SMTP host to use when sending email. If unset, the following values are tried: 1) the value of the 'mail.smtp.host' system variable, 2) localhost, 3) mailhost. | 
| bootstrap.notifications.email.email_smtp_port | SMTP port to use when sending email. Defaults to 25 | 
| bootstrap.servicebus.common_thread_pool_size | Default thread pool for component message processing. When the size of the common thread pool is zero or less, Eucalyptus uses separate thread pools for each component and a pool for dispatching. Default size = 256 threads. | 
| bootstrap.servicebus.component_thread_pool_size | Used when the size of the common thread pool is zero or less. Default size = 64 threads. | 
| bootstrap.servicebus.context_message_log_whitelist | Message patterns to match for logging. Allows selective message logging at INFO level. A list of wildcards that allows selective logging for development or troubleshooting (e.g., on request/response, on a package, on a component). Logging can impact security; do not use as a general purpose logging feature. | 
| bootstrap.servicebus.context_timeout | Message context timeout in seconds. Default = 60 seconds. | 
| bootstrap.servicebus.dispatch_thread_pool_size | Used when the size of the common thread pool is zero or less. Default size = 256 threads. | 
| bootstrap.servicebus.hup | Do a soft reset. Default = 0 (false). | 
| bootstrap.timer.rate | Amount of time (in milliseconds) before a previously running instance which is not reported will be marked as terminated. | 
| bootstrap.topology.coordinator_check_backoff_secs | Backoff between service state checks (in seconds). | 
| bootstrap.topology.local_check_backoff_secs | Backoff between service state checks (in seconds). | 
| bootstrap.tx.concurrent_update_retries | Maximum number of times a transaction may be retried before giving up. | 
| bootstrap.webservices.async_internal_operations | Execute internal service operations from a separate thread pool (with respect to I/O). | 
| bootstrap.webservices.async_operations | Execute service operations from a separate thread pool (with respect to I/O). | 
| bootstrap.webservices.async_pipeline | Execute service specific pipeline handlers from a separate thread pool (with respect to I/O). | 
| bootstrap.webservices.channel_connect_timeout | Channel connect timeout (ms). | 
| bootstrap.webservices.channel_keep_alive | Socket keep alive. | 
| bootstrap.webservices.channel_nodelay | Server socket TCP_NODELAY. | 
| bootstrap.webservices.channel_reuse_address | Socket reuse address. | 
| bootstrap.webservices.client_http_chunk_buffer_max | Server http chunk max. | 
| bootstrap.webservices.client_idle_timeout_secs | Client idle timeout (secs). | 
| bootstrap.webservices.client_internal_timeout_secs | Client idle timeout (secs). | 
| bootstrap.webservices.client_pool_max_mem_per_conn | Server worker thread pool max. | 
| bootstrap.webservices.client_pool_max_threads | Server worker thread pool max. | 
| bootstrap.webservices.client_pool_timeout_millis | Client socket select timeout (ms). | 
| bootstrap.webservices.client_pool_total_mem | Server worker thread pool max. | 
| bootstrap.webservices.clock_skew_sec | A max clock skew value (in seconds) between client and server accepted when validating timestamps in Query/REST protocol. | 
| bootstrap.webservices.cluster_connect_timeout_millis | Cluster connect timeout (ms). | 
| bootstrap.webservices.default_aws_sns_uri_scheme | Default scheme for AWS_SNS_URL. | 
| bootstrap.webservices.default_ec2_uri_scheme | Default scheme for EC2_URL. | 
| bootstrap.webservices.default_euare_uri_scheme | Default scheme for EUARE_URL. | 
| bootstrap.webservices.default_eustore_url | Default EUSTORE_URL. | 
| bootstrap.webservices.default_https_enabled | Default scheme prefix. | 
| bootstrap.webservices.default_s3_uri_scheme | Default scheme for S3_URL. | 
| bootstrap.webservices.disabled_soap_api_components | List of services with disabled SOAP APIs. | 
| bootstrap.webservices.http_max_chunk_bytes | Maximum HTTP chunk size (bytes). | 
| bootstrap.webservices.http_max_header_bytes | Maximum HTTP headers size (bytes). | 
| bootstrap.webservices.http_max_initial_line_bytes | Maximum HTTP initial line size (bytes). | 
| bootstrap.webservices.http_server_header | HTTP server header returned for responses. If set to "default", the standard version header is returned, e.g. Eucalyptus/4.3.1. If set to another value, that value is returned in the header, except for an empty value, which results in no server header being returned.Default: default | 
| bootstrap.webservices.listener_address_match | CIDRs matching addresses to bind on Default interface is always bound regardless. | 
| bootstrap.webservices.log_requests | Enable request logging. | 
| bootstrap.webservices.oob_internal_operations | Execute internal service operations out of band from the normal service bus. | 
| bootstrap.webservices.pipeline_idle_timeout_seconds | Server socket idle time-out. | 
| bootstrap.webservices.pipeline_max_query_request_size | Maximum Query Pipeline http chunk size (bytes). | 
| bootstrap.webservices.port | Port to bind Port 8773 is always bound regardless. | 
| bootstrap.webservices.replay_skew_window_sec | Time interval duration (in seconds) during which duplicate signatures will be accepted to accommodate collisions. | 
| bootstrap.webservices.server_boss_pool_max_mem_per_conn | Server max selector memory per connection. | 
| bootstrap.webservices.server_boss_pool_max_threads | Server selector thread pool max. | 
| bootstrap.webservices.server_boss_pool_timeout_millis | Service socket select timeout (ms). | 
| bootstrap.webservices.server_boss_pool_total_mem | Server worker thread pool max. | 
| bootstrap.webservices.server_channel_nodelay | Server socket TCP_NODELAY. | 
| bootstrap.webservices.server_channel_reuse_address | Server socket reuse address. | 
| bootstrap.webservices.server_pool_max_mem_per_conn | Server max worker memory per connection. | 
| bootstrap.webservices.server_pool_max_threads | Server worker thread pool max. | 
| bootstrap.webservices.server_pool_timeout_millis | Service socket select timeout (ms). | 
| bootstrap.webservices.server_pool_total_mem | Server max worker memory total. | 
| bootstrap.webservices.statistics | Record and report service times. | 
| bootstrap.webservices.unknown_parameter_handling | Request unknown parameter handling (default | ignore | error) | 
| bootstrap.webservices.use_dns_delegation | Use DNS delegation. | 
| bootstrap.webservices.use_instance_dns | Use DNS names for instances. | 
| bootstrap.webservices.ssl.server_alias | Alias of the certificate entry in euca.p12 to use for SSL for webservices. | 
| bootstrap.webservices.ssl.server_password | Password of the private key corresponding to the specified certificate for SSL for web services. | 
| bootstrap.webservices.ssl.server_ssl_ciphers | SSL ciphers for web services. | 
| bootstrap.webservices.ssl.server_ssl_protocols | SSL protocols for web services. | 
| bootstrap.webservices.ssl.user_ssl_ciphers | SSL ciphers for external use. | 
| bootstrap.webservices.ssl.user_ssl_default_cas | Use default CAs with SSL for external use. | 
| bootstrap.webservices.ssl.user_ssl_enable_hostname_verification | SSL hostname validation for external use. | 
| bootstrap.webservices.ssl.user_ssl_protocols | SSL protocols for external use. | 
| cloud.db_check_poll_time | Poll time (ms) for db connection check | 
| cloud.db_check_threshold | Threshold (number of connections or %) for db connection check | 
| cloud.euca_log_level | Log level for dynamic override. | 
| cloud.identifier_canonicalizer | Name of the canonicalizer for resource identifiers. | 
| cloud.log_file_disk_check_poll_time | Poll time (ms) for log file disk check | 
| cloud.log_file_disk_check_threshold | Threshold (bytes or %) for log file disk check | 
| cloud.memory_check_poll_time | Poll time (ms) for memory check | 
| cloud.memory_check_ratio | Ratio (of post-garbage collected old-gen memory) for memory check | 
| cloud.trigger_fault | Fault id last used to trigger test | 
| cloud.cluster.disabledinterval | The time period between service state checks for a Cluster Controller which is DISABLED. | 
| cloud.cluster.enabledinterval | The time period between service state checks for a Cluster Controller which is ENABLED. | 
| cloud.cluster.notreadyinterval | The time period between service state checks for a Cluster Controller which is NOTREADY. | 
| cloud.cluster.pendinginterval | The time period between service state checks for a Cluster Controller which is PENDING. | 
| cloud.cluster.requestworkers | The number of concurrent requests which will be sent to a single Cluster Controller. | 
| cloud.cluster.startupsyncretries | The number of times a request will be retried while bootstrapping a Cluster Controller. | 
| cloud.images.cleanupperiod | The period between runs for clean up of deregistered images. | 
| cloud.images.defaultvisibility | The default value used to determine whether or not images are marked 'public' when first registered. | 
| cloud.images.maximagesizegb | The maximum registerable image size in GB | 
| cloud.images.maxmanifestsizebytes | The maximum allowed image manifest size in bytes | 
| cloud.monitor.default_poll_interval_mins | How often the CLC requests data from the CC. Default value is 5 minutes. | 
| cloud.monitor.history_size | How many data value samples are sent from the CC to the CLC. The default value is 5. | 
| cloud.network.address_pending_timeout | Minutes before a pending system public address allocation times out and is released. Default: 35 minutes. | 
| cloud.network.ec2_classic_additional_protocols_allowed | Comma delimited list of protocol numbers supported in EDGE mode for security group rules beyond the EC2-Classic defaults (TCP,UDP,ICMP). Only valid IANA protocol numbers are accepted. Default: None[]({{< relref "" >}}) | 
| cloud.network.max_broadcast_apply | Maximum time to apply network information. Default: 120 seconds. | 
| cloud.network.min_broadcast_interval | Minimum interval between broadcasts of network information. Default: 5 seconds. | 
| cloud.network.network_index_pending_timeout | Minutes before a pending index allocation times out and is released. Default: 35 minutes. | 
| cloud.vmstate.buried_time | Amount of time (in minutes) to retain unreported terminated instance data. | 
| cloud.vmstate.ebs_root_device_name | Name for root block device mapping | 
| cloud.vmstate.ebs_volume_creation_timeout | Amount of time (in minutes) before a EBS volume backing the instance is created | 
| cloud.vmstate.instance_reachability_timeout | Amount of time (in minutes) before a VM which is not reported by a cluster will fail a reachability test. | 
| cloud.vmstate.instance_subdomain | Subdomain to use for instance DNS. | 
| cloud.vmstate.instance_timeout | Amount of time (default unit minutes) before a previously running instance which is not reported will be marked as terminated. | 
| cloud.vmstate.instance_touch_interval | Amount of time (in minutes) between updates for a running instance. | 
| cloud.vmstate.mac_prefix | Default prefix to use for instance / network interface MAC addresses. | 
| cloud.vmstate.max_state_threads | Maximum number of threads the system will use to service blocking state changes. | 
| cloud.vmstate.migration_refresh_time | Maximum amount of time (in seconds) that migration state will take to propagate state changes (e.g., to tags). | 
| cloud.vmstate.network_metadata_refresh_time | Maximum amount of time (in seconds) that the network topology service takes to propagate state changes. | 
| cloud.vmstate.pending_time | Amount of time (in minutes) before a pending instance will be terminated. | 
| cloud.vmstate.shut_down_time | Amount of time (in minutes) before a VM which is not reported by a cluster will be marked as terminated. | 
| cloud.vmstate.stopping_time | Amount of time (in minutes) before a stopping VM which is not reported by a cluster will be marked as terminated. | 
| cloud.vmstate.terminated_time | Amount of time (in minutes) that a terminated VM will continue to be reported. | 
| cloud.vmstate.tx_retries | Number of times to retry transactions in the face of potential concurrent update conflicts. | 
| cloud.vmstate.unknown_instance_handlers | Comma separated list of handlers to use for unknown instances ('restore', 'restore-failed', 'terminate', 'terminate-done') | 
| cloud.vmstate.user_data_max_size_kb | Max length (in KB) that the user data file can be for an instance (after base 64 decoding) | 
| cloud.vmstate.vm_initial_report_timeout | Amount of time (in seconds) since completion of the creating run instance operation that the new instance is treated as unreported if not... reported. | 
| cloud.vmstate.vm_metadata_generated_cache | Instance metadata generated data cache configuration. The cache is used for IAM metadata (../latest/meta-data/iam/) and instance identity (../latest/dynamic/instance-identity/).Default: maximumSize=1000, expireAfterWrite=5m | 
| cloud.vmstate.vm_metadata_instance_cache | Instance metadata cache configuration. | 
| cloud.vmstate.vm_metadata_request_cache | Instance metadata instance resolution cache configuration. | 
| cloud.vmstate.vm_metadata_user_data_cache | Instance metadata user data cache configuration. | 
| cloud.vmstate.vm_state_settle_time | Amount of time (in seconds) to let instance state settle after a transition to either stopping or shutting-down. | 
| cloud.vmstate.volatile_state_interval_sec | Period (in seconds) between state updates for actively changing state. | 
| cloud.vmstate.volatile_state_timeout_sec | Timeout (in seconds) before a requested instance terminate will be repeated. | 
| cloud.vmtypes.default_type_name | Default type used when no instance type is specified for run instances. | 
| cloud.vmtypes.format_ephemeral_storage | Format first ephemeral disk by defaut with ext3 | 
| cloud.vpc.defaultvpc | Enable default VPC. | 
| cloud.vpc.networkaclspervpc | Maximum number of network ACLs for each VPC. | 
| cloud.vpc.routespertable | Maximum number of routes for each route table. | 
| cloud.vpc.routetablespervpc | Maximum number of route tables for each VPC. | 
| cloud.vpc.rulespernetworkacl | Maximum number of rules per direction for each network ACL. | 
| cloud.vpc.rulespersecuritygroup | Maximum number of associated security groups for each network interface . | 
| cloud.vpc.securitygroupspernetworkinterface | Maximum number of associated security groups for each network interface . | 
| cloud.vpc.securitygroupspervpc | Maximum number of security groups for each VPC. | 
| cloud.vpc.subnetspervpc | Maximum number of subnets for each VPC. | 
| cloudformation.autoscaling_group_deleted_max_delete_retry_secs | The amount of time (in seconds) to wait for an autoscaling group to be deleted after deletion) | 
| cloudformation.autoscaling_group_zero_instances_max_delete_retry_secs | The amount of time (in seconds) to wait for an autoscaling group to have zero instances during delete | 
| cloudformation.instance_attach_volume_max_create_retry_secs | The amount of time (in seconds) to wait for an instance to have volumes attached after creation) | 
| cloudformation.instance_running_max_create_retry_secs | The amount of time (in seconds) to wait for an instance to be running after creation) | 
| cloudformation.instance_terminated_max_delete_retry_secs | The amount of time (in seconds) to wait for an instance to be terminated after deletion) | 
| cloudformation.max_attributes_per_mapping | The maximum number of attributes allowed in a mapping in a template | 
| cloudformation.max_mappings_per_template | The maximum number of mappings allowed in a template | 
| cloudformation.max_outputs_per_template | The maximum number of outputs allowed in a template | 
| cloudformation.max_parameters_per_template | The maximum number of outputs allowed in a template | 
| cloudformation.max_resources_per_template | The maximum number of resources allowed in a template | 
| cloudformation.region | The value of AWS::Region and value in CloudFormation ARNs for Region | 
| cloudformation.request_template_body_max_length_bytes | The maximum number of bytes in a request-embedded template | 
| cloudformation.request_template_url_max_content_length_bytes | The maximum number of bytes in a template referenced via a URL | 
| cloudformation.security_group_max_delete_retry_secs | The amount of time (in seconds) to retry security group deletes (may fail if instances from autoscaling group) | 
| cloudformation.subnet_max_delete_retry_secs | The amount of time (in seconds) to retry subnet deletes | 
| cloudformation.swf_activity_worker_config | JSON configuration for the cloudformation simple workflow activity worker | 
| cloudformation.swf_domain | The simple workflow service domain for cloudformation | 
| cloudformation.swf_tasklist | The simple workflow service task list for cloudformation | 
| cloudformation.url_domain_whitelist | A comma separated white list of domains (other than Eucalyptus S3 URLs) allowed by CloudFormation URL parameters | 
| cloudformation.volume_attachment_max_create_retry_secs | The amount of time (in seconds) to wait for a volume to be attached during create) | 
| cloudformation.volume_available_max_create_retry_secs | The amount of time (in seconds) to wait for a volume to be available after create) | 
| cloudformation.volume_deleted_max_delete_retry_secs | The amount of time (in seconds) to wait for a volume to be deleted) | 
| cloudformation.volume_detachment_max_delete_retry_secs | The amount of time (in seconds) to wait for a volume to detach during delete) | 
| cloudformation.volume_snapshot_complete_max_delete_retry_secs | The amount of time (in seconds) to wait for a snapshot to be complete (if specified as the deletion policy) before a volume is deleted) | 
| cloudformation.wait_condition_bucket_prefix | The prefix of the bucket used for wait condition handles | 
| cloudwatch.disable_cloudwatch_service | Set this to true to stop cloud watch alarm evaluation and new alarm/metric data entry | 
| dns.dns_listener_address_match | Additional address patterns to listen on for DNS requests. | 
| dns.enabled | Enable pluggable DNS resolvers. This must be 'true' for any pluggable resolver to work. Also, each resolver may need to be separately enabled. | 
| dns.search | Comma separated list of domains to search, OS settings used if none specified (a change requires restart). | 
| dns.server | Comma separated list of name servers; OS settings used if none specified (change requires restart) | 
| dns.server_pool_max_threads | Server worker thread pool max. | 
| dns.server_pool_max_threads | Server worker thread pool max. | 
| dns.instancedata.enabled | Enable the instance-data resolver. dns.enabled must also be 'true'. | 
| dns.ns.enabled | Enable the NS resolver. dns.enabled must also be 'true'. | 
| dns.recursive.enabled | Enable the recursive DNS resolver. dns.enabled must also be 'true'. | 
| dns.services.enabled | Enable the service topology resolver. dns.enabled must also be 'true'. | 
| dns.split_horizon.enabled | Enable the split-horizon DNS resolution for internal instance public DNS name queries. dns.enabled must also be 'true'. | 
| dns.spoof_regions.enabled | Enable the spoofing resolver which allows for AWS DNS name emulation for instances. | 
| dns.spoof_regions.region_name | Internal region name. If set, the region name to expect as the second label in the DNS name. For example, to treat your Eucalyptus install like a region named 'eucalyptus', set this value to eucalyptus. Then, e.g., autoscaling.eucalyptus.amazonaws.com will resolve to the service address when using this DNS server. The specified name creates a pseudo-region with DNS names like ec2.pseudo-region.amazonaws.com will resolve to Eucalyptus endpoints from inside of instances. Here ec2 is any service name supported by Eucalyptus. Those that are not supported will continue to resolve through AWS's DNS. | 
| dns.spoof_regions.spoof_aws_default_regions | Enable spoofing of the default AWS DNS names, e.g., ec2.amazonaws.com would resolve to the ENABLED Cloud Controller. Here ec2 is any service name supported by Eucalyptus. Those that are not supported will continue to resolve through AWS's DNS. | 
| dns.spoof_regions.spoof_aws_regions | Enable spoofing for the normal AWS regions, e.g., ec2.us-east-1.amazonaws.com would resolve to the ENABLED Cloud Controller. Here ec2 is any service name supported by Eucalyptus. Those that are not supported will continue to resolve through AWS's DNS. | 
| dns.tcp.timeout_seconds | Variable controlling tcp handler timeout in seconds. | 
| objectstorage.bucket_creation_wait_interval_seconds | Interval, in seconds, during which buckets in creating-state are valid. After this interval, the operation is assumed failed. | 
| objectstorage.bucket_naming_restrictions | The S3 bucket naming restrictions to enforce. Values are 'dns-compliant' or 'extended'. Default is 'extended'. dns_compliant is non-US region S3 names, extended is for US-Standard Region naming. See  http://docs.aws.amazon.com/AmazonS3/latest/dev/BucketRestrictions.html.[]({{< relref "" >}}) | 
| objectstorage.cleanup_task_interval_seconds | Interval, in seconds, at which cleanup tasks are initiated for removing old/stale objects. | 
| objectstorage.dogetputoncopyfail | Should provider client attempt a GET / PUT when backend does not support Copy operation | 
| objectstorage.failed_put_timeout_hrs | Number of hours to wait for object PUT operations to be allowed to complete before cleanup. | 
| objectstorage.max_buckets_per_account | Maximum number of buckets per account | 
| objectstorage.max_total_reporting_capacity_gb | Total ObjectStorage storage capacity for Objects solely for reporting usage percentage. Not a size restriction. No enforcement of this value | 
| objectstorage.providerclient | Object Storage Provider client to use for backend | 
| objectstorage.queue_size | Channel buffer queue size for uploads | 
| objectstorage.queue_timeout | Channel buffer queue timeout (in seconds) | 
| objectstorage.s3client.buffer_size | Internal S3 client buffer size | 
| objectstorage.s3client.connection_timeout_ms | Internal S3 client connection timeout in ms | 
| objectstorage.s3client.max_connections | Internal S3 client maximum connections | 
| objectstorage.s3client.max_error_retries | Internal S3 client maximum retries on error | 
| objectstorage.s3client.socket_read_timeout_ms | Internal S3 client socket read timeout in ms | 
| objectstorage.s3provider.s3accesskey | Local Store S3 Access Key. | 
| objectstorage.s3provider.s3endpoint | External S3 endpoint. | 
| objectstorage.s3provider.s3secretkey | Local Store S3 Secret Key. | 
| objectstorage.s3provider.s3usebackenddns | Use DNS virtual-hosted-style bucket names for communication to service backend. | 
| objectstorage.s3provider.s3usehttps | Use HTTPS for communication to service backend. | 
| region.region_enable_ssl | Enable SSL (HTTPS) for regions. | 
| region.region_name | Region name. | 
| region.region_ssl_ciphers | Ciphers to use for region SSL | 
| region.region_ssl_default_cas | Use default CAs for region SSL connections. | 
| region.region_ssl_protocols | Protocols to use for region SSL | 
| region.region_ssl_verify_hostnames | Verify hostnames for region SSL connections. | 
| reporting.data_collection_enabled | Set this to false to stop reporting from populating new data. | 
| reporting.default_size_time_size_unit | Default size-time size unit (GB-days, etc) | 
| reporting.default_size_time_time_unit | Default size-time time unit (GB-days, etc) | 
| reporting.default_size_unit | Default size unit | 
| reporting.default_time_unit | Default time unit | 
| reporting.default_write_interval_mins | How often the reporting system requests information from the Cluster Controller | 
| services.database.appendonlyhost | host address of the backend database for append-only data | 
| services.database.appendonlypassword | password of the backend database for append-only data | 
| services.database.appendonlyport | port number of the backend database for append-only data | 
| services.database.appendonlysslcert | ssl certificate to use when connecting to the backend database for append-only data | 
| services.database.appendonlyuser | user name of the backend database for append-only data | 
| services.imaging.import_task_expiration_hours | expiration hours of import volume/instance tasks | 
| services.imaging.import_task_timeout_minutes | expiration time in minutes of import tasks | 
| services.imaging.worker.availability_zones | availability zones for imaging worker | 
| services.imaging.worker.configured | Prepare imaging service so a worker can be launched. If something goes south with the service there is a big chance that setting it to false and back to true would solve issues. | 
| services.imaging.worker.expiration_days | the days after which imaging work VMs expire | 
| services.imaging.worker.healthcheck | enabling imaging worker health check | 
| services.imaging.worker.image | EMI containing imaging worker | 
| services.imaging.worker.init_script | bash script that will be executed before service configuration and start up | 
| services.imaging.worker.instance_type | instance type for imaging worker | 
| services.imaging.worker.keyname | keyname to use when debugging imaging worker | 
| services.imaging.worker.log_server | address/ip of the server that collects logs from imaging wokrers | 
| services.imaging.worker.log_server_port | UDP port that log server is listening to | 
| services.imaging.worker.log_server_port | UDP port that log server is listening to | 
| services.imaging.worker.ntp_server | address of the NTP server used by imaging worker | 
| services.loadbalancing.dns_resolver_enabled | Enable the load balancing DNS resolver. dns.enabled must also be 'true'. | 
| services.loadbalancing.dns_subdomain | loadbalancer dns subdomain | 
| services.loadbalancing.dns_ttl | loadbalancer dns ttl value | 
| services.loadbalancing.restricted_ports | The ports restricted for use as a loadbalancer port. Format should be port(, port) or port-port | 
| services.loadbalancing.vm_per_zone | number of VMs per loadbalancer zone | 
| services.loadbalancing.worker.app_cookie_duration | duration of app-controlled cookie to be kept in-memory (hours) | 
| services.loadbalancing.worker.expiration_days | the days after which the loadbalancer VMs expire | 
| services.loadbalancing.worker.image | EMI containing haproxy and the controller | 
| services.loadbalancing.worker.init_script | bash script that will be executed before service configuration and start up | 
| services.loadbalancing.worker.instance_type | instance type for loadbalancer instances | 
| services.loadbalancing.worker.keyname | keyname to use when debugging loadbalancer VMs | 
| services.loadbalancing.worker.ntp_server | the address of the NTP server used by loadbalancer VMs | 
| services.simpleworkflow.activitytypesperdomain | Maximum number of activity types for each domain. | 
| services.simpleworkflow.deprecatedactivitytyperetentionduration | Deprecated activity type retention time. | 
| services.simpleworkflow.deprecateddomainretentionduration | Deprecated domain minimum retention time. | 
| services.simpleworkflow.deprecatedworkflowtyperetentionduration | Deprecated workflow type minimum retention time. | 
| services.simpleworkflow.openactivitytasksperworkflowexecution | Maximum number of open activity tasks for each workflow execution. | 
| services.simpleworkflow.opentimersperworkflowexecution | Maximum number of open timers for each workflow execution. | 
| services.simpleworkflow.openworkflowexecutionsperdomain | Maximum number of open workflow executions for each domain. | 
| services.simpleworkflow.systemonly | Service available for internal/administrator use only. | 
| services.simpleworkflow.workflowexecutionduration | Maximum workflow execution time. | 
| services.simpleworkflow.workflowexecutionhistorysize | Maximum number of events per workflow execution. | 
| services.simpleworkflow.workflowexecutionretentionduration | Maximum workflow execution history retention time. | 
| services.simpleworkflow.workflowtypesperdomain | Maximum number of workflow types for each domain. | 
| stats.config_update_check_interval_seconds | Interval, in seconds, at which the sensor configuration is checked for changes | 
| stats.enable_stats | Enable Eucalyptus internal monitoring stats | 
| stats.event_emitter | Internal stats emitter FQ classname used to send metrics to monitoring system | 
| stats.file_system_emitter.stats_data_permissions | group permissions to place on stats data files in string form. eg. rwxr-x--x | 
| stats.file_system_emitter.stats_group_name | group name that owns stats data files | 
| storage.global_total_snapshot_size_limit_gb | Maximum total snapshot capacity (GB) | 
| system.dns.dnsdomain | Domain name to use for DNS. | 
| system.dns.nameserver | Nameserver hostname. | 
| system.dns.nameserveraddress | Nameserver IP address. | 
| system.dns.nameserveraddress | Nameserver IP address. | 
| system.dns.registrationid | Unique ID of this cloud installation. | 
| system.exec.io_chunk_size | Size of IO chunks for streaming IO | 
| system.exec.max_restricted_concurrent_ops | Maximum number of concurrent processes which match any of the patterns in system.exec.restricted_concurrent_ops. | 
| system.exec.restricted_concurrent_ops | Comma-separated list of commands which are restricted by system.exec.max_restricted_concurrent_ops. | 
| tagging.max_tags_per_resource | The maximum number of tags per resource for each account | 
| tokens.disabledactions | Actions to disable | 
| tokens.enabledactions | Actions to enable (ignored if empty) | 
| tokens.rolearnaliaswhitelist | Permitted account aliases for role Amazon Resource Names (ARNs). Value is a list, for example: eucalyptus,aws,dev*,prod* in the case where multiple aliases are permitted. Default: eucalyptus | 
| tokens.webidentityoidcdiscoverycache | Cache settings for discovered OpenID Connect metadata: provider configuration and keys. Works with tokens.webidentityoidcdiscoveryrefresh. Default: maximumSize=20, expireAfterWrite=15m | 
| tokens.webidentityoidcdiscoveryrefresh | OpenID Connect discovery cache refresh expiry. Controls the time in seconds between checks for updated OIDC metadata. Works with tokens.webidentityoidcdiscoverycache. Default: 60 | 
| tokens.webidentitysignaturealgorithmwhitelist | List of JSON Web Signature algorithms to allow in web identity tokens. The algorithm whitelist can be used to permit use of these signature algorithms: RS256, RS384, RS512, PS256, PS384, PS512. Default: RS512 | 
| tokens.webidentitytokenskew | A clock skew value in seconds. The Web identity token expiry / not before validation is allowed within the configured skew. Default: 60 | 
| walrusbackend.blockdevice | DRBD block device | 
| walrusbackend.resource | DRBD resource name | 
| walrusbackend.storagedir | Path to buckets storage | 
| walrusbackend.storagemaxtotalcapacity | Total WalrusBackend storage capacity for Objects | 
| ZONE.cluster.networkmode | Currently configured network mode. Default: None | 
| ZONE.cluster.sourcehostname | Alternative address which is the source address for requests made by the component to the cloud controller. Default: None | 
| ZONE.cluster.vnetnetmask | Netmask used by the cluster's virtual private networking. Default: None | 
| ZONE.cluster.vnetsubnet | IP subnet used by the cluster's virtual private networking. Default: None | 
| ZONE.cluster.vnettype | IP version used by the cluster's virtual private networking. Default: None | 
| ZONE.storage.blockstoragemanager | EBS Block Storage Manager to use for backend | 
| ZONE.storage.cephconfigfile | Absolute path to Ceph configuration (ceph.conf) file. Default value is '/etc/ceph/ceph.conf' | 
| ZONE.storage.cephkeyringfile | Absolute path to Ceph keyring (ceph.client.eucalyptus.keyring) file. Default value is '/etc/ceph/ceph.client.eucalyptus.keyring' | 
| ZONE.storage.cephsnapshotpools | Ceph storage pool(s) made available to Eucalyptus for EBS snapshots. Use a comma separated list for configuring multiple pools. Default value is 'rbd' | 
| ZONE.storage.cephuser | Ceph username employed by Eucalyptus operations. Default value is 'eucalyptus' | 
| ZONE.storage.cephvolumepools | Ceph storage pool(s) made available to Eucalyptus for EBS volumes. Use a comma separated list for configuring multiple pools. Default value is 'rbd' | 
| ZONE.storage.chapuser | User ID for CHAP authentication | 
| ZONE.storage.dasdevice | Direct attached storage device location | 
| ZONE.storage.maxconcurrentsnapshots | Maximum number of snapshots processed on the block storage backend at a given time | 
| ZONE.storage.maxconcurrentsnapshottransfers | Maximum number of snapshots that can be uploaded to or downloaded from objectstorage gateway at a given time | 
| ZONE.storage.maxconcurrentvolumes | Maximum number of volumes processed on the block storage backend at a given time | 
| ZONE.storage.maxsnapshotdeltas | A non-zero integer value enables upload of incremental snapshots when possible. The configured value indicates the SC to create/upload that many snapshot deltas for a given EBS volume before triggering a full upload of the snapshot contents. Between any two consecutive full snapshot uploads for a given EBS volume, there will be at most maxsnapshotdeltas number of incremental snapshot uploads. A value of 0 indicates that a newly created snapshot will always be uploaded in its entirety (that is, no deltas). Snapshot deltas are only used when your backend is Ceph-RBD. ZONE.storage.shouldtransfersnapshots must be set to true to enable snapshot deltas.Default: 0 | 
| ZONE.storage.maxsnapshotpartsqueuesize | Maximum number of snapshot parts per snapshot that can be spooled on the disk | 
| ZONE.storage.maxtotalvolumesizeingb | Total disk space reserved for volumes | 
| ZONE.storage.maxvolumesizeingb | Max volume size | 
| ZONE.storage.ncpaths | iSCSI Paths for NC. Default value is 'nopath' | 
| ZONE.storage.readbuffersizeinmb | Buffer size in MB for reading data from snapshot when uploading snapshot to objectstorage gateway | 
| ZONE.storage.resourceprefix | Prefix for resource name on SAN | 
| ZONE.storage.resourcesuffix | Suffix for resource name on SAN | 
| ZONE.storage.sanhost | Hostname for SAN device. | 
| ZONE.storage.sanpassword | Password for SAN device. | 
| ZONE.storage.sanuser | Username for SAN device. | 
| ZONE.storage.scpaths | iSCSI Paths for SC. Default value is 'nopath' | 
| ZONE.storage.shouldtransfersnapshots | Enable snapshot transfer to the OSG. Setting it to false will disable storing snapshots (full or delta) in object storage. While a false setting will reduce object storage requirements, it also prevents the ability to use a snapshot from one availability zone to create a volume in another zone. You can still take/use snapshots even when the setting is false, but you can only use a snapshot to create a volume in the same zone. Must be set to true to use snapshot deltas, which are managed by the ZONE.storage.maxsnapshotdeltas property.Default: true | 
| ZONE.storage.snapexpiration | Time interval in minutes after which Storage Controller metadata for snapshots that have been physically removed from the block storage backend will be deleted | 
| ZONE.storage.snapshotpartsizeinmb | Snapshot part size in MB for snapshot transfers using multipart upload. Minimum part size is 5MB | 
| ZONE.storage.snapshottransfertimeoutinhours | Snapshot upload wait time in hours after which the upload will be cancelled | 
| ZONE.storage.storeprefix | Prefix for ISCSI device | 
| ZONE.storage.tasktimeout | Timeout for SAN commands. | 
| ZONE.storage.tid | Next Target ID for ISCSI device | 
| ZONE.storage.timeoutinmillis | Timeout value in milli seconds for storage operations | 
| ZONE.storage.volexpiration | Time interval in minutes after which Storage Controller metadata for volumes that have been physically removed from the block storage backend will be deleted | 
| ZONE.storage.volumesdir | Storage volumes directory. | 
| ZONE.storage.writebuffersizeinmb | Buffer size in MB for writing data to snapshot when downloading snapshot from object storage gateway | 
| ZONE.storage.zerofillvolumes | Should volumes be zero filled. | 

