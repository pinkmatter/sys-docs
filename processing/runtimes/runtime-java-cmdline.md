# Java command-line runtime configuration

> Back to the [Runtimes Page](runtimes.md)

## Example configuration

```json
{
    "id": "farearth.local-cmdline",
    "type": "java-cmdline",
    "deactivated": true,
    "enabledExecutors": [
        "diagnostics:1.0.12"
    ],
    "properties": {
        "jsonPluginsFolderPath": "../../../../../farearth-plugins/src/capabilities"
    }
}
```