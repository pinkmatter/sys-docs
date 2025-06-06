# Google Drive Pickup configuration

> Back to the [Pickup Page](pickups.md)

## Example configuration

```json
{
    "id": "farearth.clienta-satname-1-pickup",
    "protocol": "gdrive",
    "dataRetentionWindow": "12 hours",
    "shareable": true,
    "attachParameters": {
        "workflowId": "farearth.clienta",
        "sendNotification": true
    },
    "triggers": [
        {
            "subscriptionId": "clienta",
            "id": "FILE_MANIFEST"
        },
        {
            "subscriptionId": "clienta",
            "id": "NO_CHANGE",
            "delay": "5m",
            "miniumFileCount": 1
        }        
    ],        
    "properties": {
        "credFileB64": "...",
        "watchFolder": "ClientA/Pickup RAW/FarEarth SATNAME-1 Pickup",
        "cacheFolder": "ClientA/Pickup RAW/Cache"
    }
}
```