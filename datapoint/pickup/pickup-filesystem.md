# Filesystem Pickup configuration

> Back to the [Pickup Page](pickups.md)

## Example configuration

```json
{
    "id": "farearth.fs-pickup-101",
    "protocol": "filesystem",
    "attachParameters": {
        "workflowId": "farearth.archive",
        "sendNotification": true
    },
    "triggers": [
        {
            "subscriptionId": "farearth",
            "id": "READY_FILE"
        },
        {
            "subscriptionId": "farearth",
            "id": "PRODUCT_FILE"
        }        
    ],    
    "properties": {
        "storeDirectory": "farearth.fs-pickup-0"
    }
}
```