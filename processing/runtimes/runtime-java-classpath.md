# Java classpath runtime configuration

> Back to the [Runtimes Page](runtimes.md)

## Example configuration

```json
{
    "id": "farearth.local-classpath",
    "type": "java-classpath",
    "enabledExecutors": [
        "test_processor:1.0.12",
        "single_to_multi:1.0.12"
    ],
    "properties": {
        "jsonPluginsFolderPath": "../../../../../farearth-plugins/src/capabilities"
    }
}
```