# Filesystem Pickup configuration

##### [Home](../../README.md) > [Datapoint](../datapoint.md) > [Pickup](pickups.md) > Filesystem
---

Below is an example of a *FarEarth* [Pickup](pickups.md) configuration, for local storage.

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
        }     
    ],    
    "properties": {
        "storeDirectory": "farearth.fs-pickup-0"
    }
}
```
The required properties for the local file system protocol are:

| Field | Details |
|-------|---------|
| `storeDirectory`    | Path to local storage directly accessible by the *FarEarth* service. |

> **Note**: This configuration is typically used on self-hosted bundled deployments, where the *FarEarth* instance is packaged as a single executable.