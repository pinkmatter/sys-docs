# Filesystem configuration

##### [Home](../../README.md) > [Processing](../processing.md) > [Hosting](hosting.md) > Filesystem
---

Below is an example of a *FarEarth* [Hosting](hosting.md) configuration, for local storage.

```json
{
    "id": "fs-archive-101",
    "protocol": "filesystem",
    "properties": {
        "storeDirectory": "cache/blob/host"
    }
}
```
The required properties for the local file system protocol are:

| Field | Details |
|-------|---------|
| `storeDirectory`    | Path to local storage directly accessible by the *FarEarth* service. |

> **Note**: This configuration is typically used on self-hosted bundled deployments, where the *FarEarth* instance is packaged as a single executable.