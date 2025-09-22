# valheim

![Version: 1.0.0](https://img.shields.io/badge/Version-1.0.0-informational?style=flat-square) ![Type: application](https://img.shields.io/badge/Type-application-informational?style=flat-square) ![AppVersion: 3.3](https://img.shields.io/badge/AppVersion-3.3-informational?style=flat-square)

A Helm chart for deploying Valheim Dedicated Server

## Maintainers

| Name | Email | Url |
| ---- | ------ | --- |
| algo7 |  | <https://github.com/algo7> |

## Requirements

Kubernetes: `>=1.30.0-0`

## Values

| Key | Type | Default | Description |
|-----|------|---------|-------------|
| image.repository | string | `"ghcr.io/mbround18/valheim"` | The repository to pull the image from. |
| image.pullPolicy | string | `"IfNotPresent"` | The image pull policy. One of Always, IfNotPresent, or Never. |
| image.tag | string | `""` | Overrides the image tag whose default is the chart appVersion. |
| imagePullSecrets | list | `[]` | This is for the secrets for pulling an image from a private repository. It's likely that you won't need to change this. |
| nameOverride | string | `""` | Overrides the name of the chart. So it becomes release-name-<nameOverride> instead of release-name-chart-name. |
| fullnameOverride | string | `""` | Overrides the full name of the chart. So it becomes <fullnameOverride> |
| podAnnotations | object | `{}` | Add custom annotations to the pod. |
| podLabels | object | `{}` | Add custom labels to the pod. |
| resources | object | `{}` | Resource requests and limits |
| service.type | string | `"LoadBalancer"` | Kubernetes Service type. Supported options are ClusterIP, NodePort, and LoadBalancer. You will likely use either LoadBalancer or NodePort. |
| service.port | int | `2456` | The port the service will be exposed on. This is independent of the container port which is will always be 2456, 2457, and 2458. This will be the port you connect to. There will be 2 additional ports opened for game traffic. It's the port here +1 and +2. So if you set this to 2456, the ports opened will be 2456, 2457, and 2458. It's templated in the chart to make this easier. |
| persistence.enabled | bool | `false` | Enable persistence using a PersistentVolumeClaim. If false, an emptyDir volume is used which means all data will be lost when the pod is removed or restarted. |
| persistence.existingClaim | string | `""` | If you want to use an existing claim, specify the claim name here. If this is set, the other settings for persistence are ignored. |
| persistence.storageClassName | string | `"standard"` | StorageClass for dynamically provisioned PersistentVolume. If persistence.existingClaim is set, these values are ignored. |
| persistence.accessModes | list | `["ReadWriteOnce"]` | Access mode for the PersistentVolumeClaim. If persistence.existingClaim is set, these values are ignored. |
| persistence.size | string | `"10Gi"` | Size of the PersistentVolume. If persistence.existingClaim is set, these values are ignored. |
| nodeSelector | object | `{}` | The node selector for pod assignment |
| tolerations | list | `[]` | Tolerations for pod assignment |
| affinity | object | `{}` | Affinity for pod assignment |
| serviceAccount.create | bool | `true` | Specifies whether a service account should be created. It's a security best practice to create a dedicated service account for each application. If create is set to false, then the default service account will be used which is not recommended. |
| serviceAccount.automount | bool | `true` | Automatically mount a ServiceAccount token for the pod |
| serviceAccount.annotations | object | `{}` | Annotations to add to the service account |
| serviceAccount.name | string | `""` | The name of the service account to use. If not set and create is true, a name will be the fullname of the chart (release-name-chart-name). |
| config.data | object | `{}` | List of environment variables to set in the container. See https://github.com/mbround18/valheim-docker?tab=readme-ov-file#environment-variables for all available environment variables. |

