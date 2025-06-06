# AWS S3 Pickup configuration

> Back to the [Pickup Page](pickups.md)

## Example configuration

```json
{
    "id": "farearth.minio-s3-pickup-101",
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

## Example configuration (with SQS trigger)

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
        "accessKey": "AKIAQCLG27NFUH3FFZ6A",
        "secretKey": "gG...CY",
        "sqsQueueUrl": "https://sqs.eu-west-2.amazonaws.com/003237515848/farearthqueue"
    }
}
```