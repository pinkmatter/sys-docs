# AWS S3 configuration

> Back to the [Hosting Page](hosting.md)

## Example configuration

```json
{
    "id": "farearth.aws-s3-host-101",
    "protocol": "amazon-s3",
    "dataRetentionWindow": "12 hours",
    "properties": {
        "baseUrl": "...",
        "bucketName": "hosting",
        "region": "...",
        "accessKey": "...",
        "secretKey": "..."
    }
}
```