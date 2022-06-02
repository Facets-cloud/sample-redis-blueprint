# Some list of redis-cluster examples below:
1. [Redis-cluster with persistence storage, metrics enabled, resource limit for cpu and memory](https://github.com/Facets-cloud/sample-redis-blueprint/edit/master/README.md#example-1-redis-cluster-with-persistence-storage-metrics-enabled-resource-limit-for-cpu-and-memory)
2. [Redis-cluster with external access enabled with internet-facing load-balancers](https://github.com/Facets-cloud/sample-redis-blueprint/edit/master/README.md#example-2-redis-cluster-with-external-access-enabled-with-internet-facing-load-balancers-aws-and-azure)
3. [Redis-cluster with external access enabled with internal load-balancers(AWS)](https://github.com/Facets-cloud/sample-redis-blueprint/edit/master/README.md#example-3-redis-cluster-with-external-access-enabled-with-internal-load-balancersaws)
4. [Redis-cluster with external access enabled with internal load-balancers(Azure)](https://github.com/Facets-cloud/sample-redis-blueprint/edit/master/README.md#example-4-redis-cluster-with-external-access-enabled-with-internal-load-balancersazure)


### Example 1: Redis-cluster with persistence storage, metrics enabled, resource limit for cpu and memory


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


### Example 2: Redis-cluster with external access enabled with internet-facing load-balancers (AWS and Azure)

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
        "name": "cluster.externalAccess.enabled",
        "type": "static",
        "attribute": "true"
      }
    ]
  }
}
```


### Example 3: Redis-cluster with external access enabled with internal load-balancers(AWS)


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
      ,
      {
        "name": "cluster.externalAccess.enabled",
        "type": "static",
        "attribute": "true"
      },
      {
        "name": "cluster.externalAccess.service.annotations",
        "type": "static",
        "attribute": "service.beta.kubernetes.io/aws-load-balancer-internal: \"true\""
      }
    ]
  }
}
```


### Example 4: Redis-cluster with external access enabled with internal load-balancers(Azure)


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
      ,
      {
        "name": "cluster.externalAccess.enabled",
        "type": "static",
        "attribute": "true"
      },
      {
        "name": "cluster.externalAccess.service.annotations",
        "type": "static",
        "attribute": "service.beta.kubernetes.io/azure-load-balancer-internal: \"true\""
      }
    ]
  }
}
```
