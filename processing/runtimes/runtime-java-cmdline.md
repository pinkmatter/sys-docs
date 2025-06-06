# Java command-line runtime configuration

##### [Home](../../README.md) > [Processing](../processing.md) > [Runtimes](runtimes.md) > Cmdline
---

Below is an example of a Java processor that can be started by the *FarEarth* Processor app, as a separate process. For this runtime, the code for the Executor must be compiled into the processor app already.

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