# Azure Archive configuration

> Back to the [Archive Page](archives.md)

## Example configuration

```json
{
    "id": "farearth.azure-archive-101",
    "protocol": "azure",
    "prefix": "FarEarth-Testing/{subscription}/{year}/{doy}/{uuid}",
    "shareable": true,
    "dataStoreLimits": {
        "capacity": "64GB",
        "warnOnRemaining": "4GB",
        "errorOnRemaining": "2GB"
    },
    "properties": {
        "containerName": "archive",
        "baseUrl": "...",
        "connectionString": "..."
    }
}
```