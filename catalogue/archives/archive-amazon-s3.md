# Amazon S3 Archive configuration

##### [Home](../../README.md) > [Catalogue](../catalogue.md) > [Archive](archives.md) > Amazon S3
---

Below is an example of a *FarEarth* [Archive](archives.md) configuration, for Amazon's S3 buckets.

```json
{
    "id": "farearth.aws-s3-archive-101",
    "protocol": "amazon-s3",
    "accessModes": ["PUSH","PULL"],
    "properties": {
        "baseUrl": "...",
        "bucketName": "mynewbucket",
        "region": "...",
        "accessKey": "...",
        "secretKey": "..."
    }
}
```
The required properties for the Amazon S3 bucket are:

| Field | Details |
|-------|---------|
| `baseUrl`    | Base URL (hostname) of the bucket, as provided by Amazon |
| `bucketName` | Name of the bucket as it is configured on Amazon |
| `region`     | Region where the bucket is hosted, as provided by Amazon |
| `accessKey`  | Access key to connect to the bucket, as provided by Amazon |
| `secretKey`  | Secure secret key to the bucket, as provided by Amazon |

*FarEarth* uses a secure data transfer mechanism, where the access credentials, including the secret key, never leaves the *FarEarth* server where the key is configured (e.g., the Gateway). This means that even if other *FarEarth* components, running in other security realms, requires access to the data on the bucket, it requests the access via the Gateway, using industry standard secure communication. Data is retrieved via short-lived, access-constrained, and pre-signed URLs.
