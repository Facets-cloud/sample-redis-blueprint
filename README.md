# sample-redis-blueprint

Example 1: redis-cluster with persistence storage, metrics enabled, resource limit for cpu and memory


```
{
  "disabled": true,
  "$schema": "https://docs.facets.cloud/schemas/helm/instances/helm.schema",
  "flavor": "helm_simple",
  "spec": {
    "helm": {
      "chart": "redis-cluster",
      "repository": "https://charts.bitnami.com/bitnami",
      "wait": true,
      "version": "7.5.7"
    },
    "env": [
      {
        "name": "metrics.serviceMonitor.enabled",
        "type": "static",
        "attribute": "true"
      },
      {
        "name": "persistence.size",
        "type": "static",
        "default": "10Gi"
      },
      {
        "name": "resources.limits.cpu",
        "type": "static",
        "attribute": "100m"
      },
      {
        "name": "resources.limits.memory",
        "type": "static",
        "attribute": "128Mi"
      }
    ]
  }
}
```
