# Azure Pickup configuration

##### [Home](../../README.md) > [Datapoint](../datapoint.md) > [Pickup](pickups.md) > Azure
---

Below is an example of a *FarEarth* [Pickup](pickups.md) configuration for Microsoft Azure's blob storage.

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
The required properties for the Azure blob storage are:

| Field | Details |
|-------|---------|
| `containerName` | Name of the container as it is configured on Azure |
| `baseUrl`    | Base URL (hostname) of the container, as provided by Microsoft |
| `connectionString`  | Secure connection string used to access the container, as provided by Microsoft |

*FarEarth* uses a secure data transfer mechanism, where the access credentials, including the connectionString, never leaves the *FarEarth* server where it is configured (e.g., the Gateway). This means that even if other *FarEarth* components, running in other security realms, requires access to the data in the container, it requests the access via the Gateway, using industry standard secure communication. Data is retrieved via short-lived, access-constrained, and pre-signed URLs.
