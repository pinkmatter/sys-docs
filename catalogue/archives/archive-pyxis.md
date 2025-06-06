# Pyxis Archive configuration

> Back to the [Archive Page](archives.md)

```
{
    "id": "farearth.pyxis-archive",
    "protocol": "pyxis",
    "displayName": "Pyxis Archive (RAW Only)",
    "prefix": "archive/{spacecraft}/{productType}/{productId}/{uuid}",
    "accessModes": [
        "PUSH",
        "PULL"
    ],
    "attachProperties": {
        "id": "{spacecraft}-{productType}-{correlationId}"
    },
    "properties": {
        "baseUrl": "https://apollo.server.local:443/",
        "box": "archive",
        "password": "loremIpsum"
    }
}
```