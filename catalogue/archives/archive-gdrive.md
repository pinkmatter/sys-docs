# Google Drive Archive configuration

##### [Home](../../README.md) > [Catalogue](../catalogue.md) > [Archive](archives.md) > Google Drive
---

Below is an example of a *FarEarth* [Archive](archives.md) configuration, for Google Drive cloud storage.

```json
{
    "id": "farearth.test-archive",
    "protocol": "gdrive",
    "prefix": "Test/FarEarth Archive/TESTING/{subscription}/{year}/{doy}/{uuid}",
    "shareable": true,
    "properties": {
        "credFileB64": "..."
    }
}
```
The required properties for the Google Drive cloud storage are:

| Field | Details |
|-------|---------|
| `credFileB64`  | Base-64 encoded credentials file, as provided by Google |

*FarEarth* uses a secure data transfer mechanism, where the access credentials, including the credFileB64, never leaves the *FarEarth* server where it is configured (e.g., the Gateway). This means that even if other *FarEarth* components, running in other security realms, requires access to the data in Google Drive cloud storage, it requests the access via the Gateway, using industry standard secure communication. Data is retrieved via short-lived, access-constrained, and pre-signed URLs.