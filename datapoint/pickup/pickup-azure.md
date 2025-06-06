# Azure Pickup configuration

> Back to the [Pickup Page](pickups.md)

## Example configuration

```json
{
    "id": "farearth.azure-pickup-101",
    "protocol": "azure",
    "dataRetentionWindow": "12 hours",
    "shareable": true,
    "dataStoreLimits": {
        "capacity": "32GB",
        "warnOnRemaining": "4GB",
        "errorOnRemaining": "2GB"
    },   
    "properties": {
        "containerName": "pickup",
        "baseUrl": "...",
        "connectionString": "..."
    }
}
```