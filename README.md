# Some list of redis-cluster examples below:
1. [Redis-cluster with persistence storage, metrics enabled, resource limit for cpu and memory](https://github.com/Facets-cloud/sample-redis-blueprint/edit/master/README.md#example-1-redis-cluster-with-persistence-storage-metrics-enabled-resource-limit-for-cpu-and-memory)
2. [Redis-cluster with external access enabled with internal load-balancers (Azure)](https://github.com/Facets-cloud/sample-redis-blueprint#example-2-redis-cluster-with-external-access-enabled-with-internal-load-balancers-azure)
3. [Redis-cluster with external access enabled with internal load-balancers (AWS)](https://github.com/Facets-cloud/sample-redis-blueprint#example-3-redis-cluster-with-external-access-enabled-with-internal-load-balancers-aws)


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
      "version": "7.6.3"
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


### Example 2: Redis-cluster with external access enabled with internal load-balancers Azure

```
{
  "disabled": false,
  "flavor": "helm_simple",
  "spec": {
    "helm": {
      "chart": "redis-cluster",
      "repository": "https://charts.bitnami.com/bitnami",
      "wait": true,
      "version": "7.6.3"
    },
    "env": [],
    "values": {
      "persistence": {
        "enabled": false
      },
      "usePassword": false,
      "cluster": {
        "externalAccess": {
          "enabled": true,
          "service": {
            "type": "LoadBalancer",
            "annotations": {
              "service.beta.kubernetes.io/azure-load-balancer-internal": "true"
            }
          }
        }
      },
      "metrics": {
        "serviceMonitor": {
          "enabled": true
        }
      }
    }
  }
}
```

then once the deployment is complete, gather the external-ip of each and service and add an overide like below to map the ip to service.

```
{
  "disabled": false,
  "flavor": "helm_simple",
  "spec": {
    "helm": {
      "chart": "redis-cluster",
      "repository": "https://charts.bitnami.com/bitnami",
      "wait": true,
      "version": "7.6.3"
    },
    "env": [],
    "values": {
      "cluster": {
        "externalAccess": {
          "enabled": true,
          "service": {
            "annotations": {
              "service.beta.kubernetes.io/azure-load-balancer-internal": "true"
            },
            "loadBalancerIP": [
              "10.111.3.158",
              "10.111.3.162",
              "10.111.3.159",
              "10.111.3.161",
              "10.111.3.160",
              "10.111.3.163"
            ],
            "type": "LoadBalancer"
          }
        }
      },
      "metrics": {
        "serviceMonitor": {
          "enabled": true
        }
      },
      "persistence": {
        "enabled": false
      },
      "usePassword": false
    }
  }
}
```

### Example 3: Redis-cluster with external access enabled with internal load-balancers AWS

```
{
  "disabled": false,
  "flavor": "helm_simple",
  "spec": {
    "helm": {
      "chart": "redis-cluster",
      "repository": "https://charts.bitnami.com/bitnami",
      "wait": true,
      "version": "7.5.7"
    },
    "env": [],
    "values": {
      "persistence": {
        "enabled": false
      },
      "usePassword": false,
      "cluster": {
        "externalAccess": {
          "enabled": true,
          "service": {
            "type": "LoadBalancer",
            "annotations": {
              "service.beta.kubernetes.io/aws-load-balancer-internal": "true"
            }
          }
        }
      },
      "metrics": {
        "serviceMonitor": {
          "enabled": true
        }
      }
    }
  }
}
```

then once the deployment is complete, gather the external-ip of each and service and add an overide like below to map the ip to service.

```
{
  "disabled": false,
  "flavor": "helm_simple",
  "spec": {
    "helm": {
      "chart": "redis-cluster",
      "repository": "https://charts.bitnami.com/bitnami",
      "wait": true,
      "version": "7.5.7"
    },
    "env": [],
    "values": {
      "usePassword": false,
      "cluster": {
        "externalAccess": {
          "enabled": true,
          "service": {
            "loadBalancerIP": [
              "internal-xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx-xxxxxxxxxx.us-east-1.elb.amazonaws.com",
              "internal-xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx-xxxxxxxxxx.us-east-1.elb.amazonaws.com",
              "internal-xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx-xxxxxxxxxx.us-east-1.elb.amazonaws.com",
              "internal-xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx-xxxxxxxxxx.us-east-1.elb.amazonaws.com",
              "internal-xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx-xxxxxxxxxx.us-east-1.elb.amazonaws.com",
              "internal-xxxxxxxxxxxxxxxxxxxxxxxxxxxxxxxx-xxxxxxxxxx.us-east-1.elb.amazonaws.com"
            ],
            "type": "LoadBalancer"
          }
        }
      }
    }
  }
}
```
