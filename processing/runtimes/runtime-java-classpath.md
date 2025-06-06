# Java classpath runtime configuration

##### [Home](../../README.md) > [Processing](../processing.md) > [Runtimes](runtimes.md) > Classpath
---

Below is an example of a Java processor running within the same JVM as the *FarEarth* Processor app. For this runtime, the code for the Executor must be compiled into the processor app already.

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

The `enabledExecutors` specify which executors within the JVM is enabled.