# Filesystem Archive configuration

##### [Home](../../README.md) > [Catalogue](../catalogue.md) > [Archive](archives.md) > Filesystem
---

Below is an example of a *FarEarth* [Archive](archives.md) configuration, for local storage.

```json
{
    "id": "fs-archive-0",
    "protocol": "filesystem",
    "accessModes": ["PULL"],
    "properties": {
        "storeDirectory": "cache/blob/archive"
    }
}
```
The required properties for the local file system protocol are:

| Field | Details |
|-------|---------|
| `storeDirectory`    | Path to local storage directly accessible by the *FarEarth* service. |

> **Note**: This configuration is typically used on self-hosted bundled deployments, where the *FarEarth* instance is packaged as a single executable.