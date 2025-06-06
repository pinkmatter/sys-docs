# AWS S3 Archive configuration

> Back to the [Archive Page](archives.md)

## Example configuration

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
