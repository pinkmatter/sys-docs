# Kubernetes runtime configuration

> Back to the [Runtimes Page](runtimes.md)

## Example configuration

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
        "yamlCredentialsBase64": "YXBpVm...ZXJlPg==",
        "jobMemoryLimitGi": 15,
        "jobCpuLimitMilli": 3500,
        "jobDiskLimitGi": 100.0,
        "registries": [
            {
                "baseUrl": "registry.domain.local:5000",
                "secure": false,
                "username": "lorem",
                "password": "ipsum"
            }
        ]
    }
}
```