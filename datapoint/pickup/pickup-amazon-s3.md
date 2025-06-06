# AWS S3 Pickup configuration

##### [Home](../../README.md) > [Datapoint](../datapoint.md) > [Pickup](pickups.md) > Amazon S3
---

Below is an example of a *FarEarth* [Pickup](pickups.md) configuration, for Amazon's S3 buckets.

```json
{
    "id": "farearth.amazon-s3-pickup-101",
    "protocol": "amazon-s3",
    "dataRetentionWindow": "12 hours",
    "shareable": true,    
    "properties": {
        "baseUrl": "...",
        "bucketName": "pickup",
        "sqsQueueUrl": "...",
        "region": "us-east-1",
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
| `sqsQueueUrl` | An Amazon SQS queue where *FarEarth* will listed for new file events |
| `region`     | Region where the bucket is hosted, as provided by Amazon |
| `accessKey`  | Access key to connect to the bucket, as provided by Amazon |
| `secretKey`  | Secure secret key to the bucket, as provided by Amazon |

*FarEarth* uses a secure data transfer mechanism, where the access credentials, including the secret key, never leaves the *FarEarth* server where the key is configured (e.g., the Gateway). This means that even if other *FarEarth* components, running in other security realms, requires access to the data on the bucket, it requests the access via the Gateway, using industry standard secure communication. Data is retrieved via short-lived, access-constrained, and pre-signed URLs.

**Advanced example**

This example uses Amazon SQS queues.

```json
{
    "id": "farearth.aws-s3-trigger",
    "protocol": "amazon-s3",
    "dataRetentionWindow": "12 hours",
    "skipTriggerFolderListing": true,
    "readOnly": true,
    "attachParameters": {
        "workflowId": "farearth.data-workflow"
    },
    "triggers": [
        {
            "id": "ACCEPT_ALL"
        }
    ],
    "properties": {
        "baseUrl": "https://s3.eu-west-2.amazonaws.com",
        "bucketName": "bucket",
        "region": "eu-west-2",
        "accessKey": "<insert access key>",
        "secretKey": "<insert secret key>",
        "sqsQueueUrl": "https://sqs.eu-west-2.amazonaws.com/.../farearthqueue"
    }
}
```
Features of this configuration:
* Data is stored for 12 hours and then deleted by *FarEarth*
* The `farearth.data-workflow` workflow will be triggered to process
* The trigger is configured to accept all data