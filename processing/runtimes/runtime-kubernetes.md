# Kubernetes runtime configuration

##### [Home](../../README.md) > [Processing](../processing.md) > [Runtimes](runtimes.md) > Kubernetes
---

The default method to start executors with *FarEarth* are as Kubernetes containers. The example below shows such a configuration.

Communication to the containers are handled through MQTT.

The container images are retrieved from the specified container registry.

```json
{
    "id": "farearth.orion",
    "type": "kubernetes",
    "maxJobs": 5,
    "enabledExecutors": [
        "diagnostics:1.0.12",
        "ndvi:1.1.22",
    ],
    "properties": {
        "clusterId": "orion",
        "namespace": "ns-farearth",
        "configMount": "/etc/farearth/certs/incoming:/etc/farearth/certs/incoming",
        "yamlCredentialsBase64": "<insert base-64 encoded yaml credentials>",
        "jobMemoryLimitGi": 15,
        "jobCpuLimitMilli": 3500,
        "jobDiskLimitGi": 100.0,
        "registries": [
            {
                "baseUrl": "registry.domain.local:5000",
                "secure": false,
                "username": "<insert username>",
                "password": "<insert password>"
            }
        ]
    }
}
```