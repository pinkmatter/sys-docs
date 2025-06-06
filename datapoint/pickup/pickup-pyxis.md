# Pyxis Pickup configuration

##### [Home](../../README.md) > [Datapoint](../datapoint.md) > [Pickup](pickups.md) > Pyxis
---

Below is an example of a *FarEarth* [Pickup](pickups.md) configuration, for Pyxis. Pyxis is a native blob storage provider built into *FarEarth*.

> **Note**: Access to Pyxis is provided via HTTPS connections, using TLS. *FarEarth* will check the certificates of the provided URL.

```json
{
    "id": "farearth.my-pyxis-pickup-0",
    "protocol": "pyxis",
    "readOnly": true,
    "deactivated": false,
    "attachParameters": {
        "sendNotification": false
    },
    "properties": {
        "baseUrl": "https://my.server.local:443/",
        "box": "pickup",
        "password": "..."
    }
}
```
The required properties for Pyxis are:

| Field | Details |
|-------|---------|
| `baseUrl`    | Base URL (hostname) of the HTTPS endpoint |
| `box` | Name of the box as it is configured on Pyxis |
| `password`  | Secure secret to access the box, as configured on Pyxis |

*FarEarth* uses a secure data transfer mechanism, where the access credentials, including the password, never leaves the *FarEarth* server where it is configured (e.g., the Gateway). This means that even if other *FarEarth* components, running in other security realms, requires access to the data in the box, it requests the access via the Gateway, using industry standard secure communication. Data is retrieved via short-lived, access-constrained, and pre-signed URLs.