+++
title = "Use MinIO Backend"
weight = 20
+++

This topic describes how to configure MinIO as the object storage backend provider for the Object Storage Gateway (OSG).

## Prerequisites

* The UFS must be registered and enabled. 
* Install and start MinIO

For more information on MinIO installation and configuration see the [MinIO Server Documentation](https://docs.min.io/)

## To configure MinIO object storage

You must execute the steps below as a administrator. 

Configure **minio** as the storage provider using the *euctl* command: 

```bash
euctl objectstorage.providerclient=minio
```

Configure *objectstorage.s3provider.s3endpoint* to the **ip:port** of a host running the minio server: 

```bash
euctl objectstorage.s3provider.s3endpoint=<minio-host-ip>:<minio-port>
```

{{% notice note %}}
The default port for MinIO is 9000
{{% /notice %}}

Configure *objectstorage.s3provider.s3accesskey* and *objectstorage.s3provider.s3secretkey* with credentials for minio:

```bash
euctl objectstorage.s3provider.s3accesskey=<minio-accesskey>
euctl objectstorage.s3provider.s3secretkey=<minio-secretkey>
```

Configure the expected response code for minio:

```bash
euctl objectstorage.s3provider.s3endpointheadresponse=400
```

The MinIO backend and OSG are now ready for production.
