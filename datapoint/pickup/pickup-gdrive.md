# Google Drive Pickup configuration

##### [Home](../../README.md) > [Datapoint](../datapoint.md) > [Pickup](pickups.md) > Google Drive
---

Below is an example of a *FarEarth* [Pickup](pickups.md) configuration, for Google Drive cloud storage.

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

In the example above, *FarEarth* will monitor the "watch folder" for either a manifest file (first trigger) or a single file does not change after 5 minutes (second trigger).

The required properties for the Google Drive cloud storage are:

| Field | Details |
|-------|---------|
| `credFileB64` | Base-64 encoded credentials file, as provided by Google |
| `watchFolder` | Folder within the Google Drive storage account to monitor for new files |
| `cacheFolder` | Folder where data is temporarily stored while processing (to prevent duplication ingestion) |

*FarEarth* uses a secure data transfer mechanism, where the access credentials, including the credFileB64, never leaves the *FarEarth* server where it is configured (e.g., the Gateway). This means that even if other *FarEarth* components, running in other security realms, requires access to the data in Google Drive cloud storage, it requests the access via the Gateway, using industry standard secure communication. Data is retrieved via short-lived, access-constrained, and pre-signed URLs.