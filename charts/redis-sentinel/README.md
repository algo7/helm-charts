# redis-sentinel

![Version: 1.0.0](https://img.shields.io/badge/Version-1.0.0-informational?style=flat-square) ![Type: application](https://img.shields.io/badge/Type-application-informational?style=flat-square) ![AppVersion: 8.2-alpine](https://img.shields.io/badge/AppVersion-8.2--alpine-informational?style=flat-square)

A Helm chart for deploying Redis Sentinel

## Maintainers

| Name | Email | Url |
| ---- | ------ | --- |
| algo7 |  | <https://github.com/algo7> |

## Requirements

Kubernetes: `>=1.30.0-0`

## Values

| Key | Type | Default | Description |
|-----|------|---------|-------------|
| nameOverride | string | `""` | Overrides the name of the chart. So it becomes release-name-<nameOverride> instead of release-name-chart-name. |
| fullnameOverride | string | `""` | Overrides the full name of the chart. So it becomes <fullnameOverride> |
| redisSecret.name | string | `"redis-secret"` | The name of the secret that contains the Redis password. This secret must exist in the same namespace as the chart is being deployed to. The key that contains the password must be "redis-password". |
| redisSecret.key | string | `"redis-password"` | The key in the secret that contains the Redis password. |
| redis.replicaCount | int | `3` | Number of Redis nodes to deploy. This is a StatefulSet so it must be 1 or the multiple of 2 plus 1 (3, 5, 7, etc). |
| redis.image.repository | string | `"redis"` | The repository to pull the image from. |
| redis.image.pullPolicy | string | `"IfNotPresent"` | The image pull policy. One of Always, IfNotPresent, or Never. |
| redis.image.tag | string | `""` | Overrides the image tag whose default is the chart appVersion. |
| redis.imagePullSecrets | list | `[]` | This is for the secrets for pulling an image from a private repository. It's likely that you won't need to change this. |
| redis.serviceAccount.create | bool | `true` | Specifies whether a service account should be created. It's a security best practice to create a dedicated service account for each application. If create is set to false, then the default service account will be used which is not recommended. |
| redis.serviceAccount.automount | bool | `true` | Automatically mount a ServiceAccount token for the pod |
| redis.serviceAccount.annotations | object | `{}` | Annotations to add to the service account |
| redis.serviceAccount.name | string | `""` | The name of the service account to use. If not set and create is true, a name will be the fullname of the chart (release-name-chart-name)-redis. |
| redis.podAnnotations | object | `{}` | Add custom annotations to the pod. |
| redis.podLabels | object | `{}` | Add custom labels to the pod. |
| redis.podSecurityContext | object | `{}` |  |
| redis.securityContext | object | `{}` |  |
| redis.resources | object | `{}` |  |
| redis.nodeSelector | object | `{}` | The node selector for pod assignment |
| redis.tolerations | list | `[]` | Tolerations for pod assignment |
| redis.affinity | object | `{}` | Affinity for pod assignment |
| redis.clusterDomain | string | `"cluster.local"` | The cluster domain for the Kubernetes cluster. Usually this is cluster.local, but if you have a custom domain you can set it here. |
| redis.persistence.enabled | bool | `false` | Enable persistence using a PersistentVolumeClaim. If false, an emptyDir volume is used which means all data will be lost when the pod is removed or restarted. |
| redis.persistence.existingClaim | string | `""` | If you want to use an existing claim, specify the claim name here. If this is set, the other settings for dynamic provisioning are ignored. |
| redis.persistence.storageClassName | string | `"standard"` | StorageClass for dynamically provisioned PersistentVolume. If persistence.existingClaim is set, these values are ignored. |
| redis.persistence.accessModes | list | `["ReadWriteOnce"]` | Access mode for the PersistentVolumeClaim. If persistence.existingClaim is set, these values are ignored. |
| redis.persistence.size | string | `"10Gi"` | Size of the PersistentVolume. If persistence.existingClaim is set, these values are ignored. |
| haproxy.replicaCount | int | `3` | Number of Redis nodes to deploy. This is a StatefulSet so it must be 1 or the multiple of 2 plus 1 (3, 5, 7, etc). |
| haproxy.image.repository | string | `"redis"` | The repository to pull the image from. |
| haproxy.image.pullPolicy | string | `"IfNotPresent"` | The image pull policy. One of Always, IfNotPresent, or Never. |
| haproxy.image.tag | string | `""` | Overrides the image tag whose default is the chart appVersion. |
| haproxy.imagePullSecrets | list | `[]` | This is for the secrets for pulling an image from a private repository. It's likely that you won't need to change this. |
| haproxy.serviceAccount.create | bool | `true` | Specifies whether a service account should be created. It's a security best practice to create a dedicated service account for each application. If create is set to false, then the default service account will be used which is not recommended. |
| haproxy.serviceAccount.automount | bool | `true` | Automatically mount a ServiceAccount token for the pod |
| haproxy.serviceAccount.annotations | object | `{}` | Annotations to add to the service account |
| haproxy.serviceAccount.name | string | `""` | The name of the service account to use. If not set and create is true, a name will be the fullname of the chart (release-name-chart-name)-redis. |
| haproxy.podAnnotations | object | `{}` | Add custom annotations to the pod. |
| haproxy.podLabels | object | `{}` | Add custom labels to the pod. |
| haproxy.podSecurityContext | object | `{}` |  |
| haproxy.securityContext | object | `{}` |  |
| haproxy.resources | object | `{}` |  |
| haproxy.service.type | string | `"LoadBalancer"` | Kubernetes Service type. Supported options are ClusterIP, NodePort, and LoadBalancer. You will likely use either LoadBalancer or NodePort. |
| haproxy.service.port | int | `6379` | The port the service will be exposed on. This is independent of the container port which is will always be 2456, 2457, and 2458. This will be the port you connect to. There will be 2 additional ports opened for game traffic. It's the port here +1 and +2. So if you set this to 2456, the ports opened will be 2456, 2457, and 2458. It's templated in the chart to make this easier. |
| haproxy.nodeSelector | object | `{}` | The node selector for pod assignment |
| haproxy.tolerations | list | `[]` | Tolerations for pod assignment |
| haproxy.affinity | object | `{}` | Affinity for pod assignment |

