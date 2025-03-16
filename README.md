# gha-aqua-agent-deployment

## Description

Github action repository for deploying the Aqua Enforcer.

## Workflow options

This section is for organising the individual GHA workflows.

### generic.yml

The features of the generic.yml:

1. The code is cloud-agnostic. It can be used to deploy on any K8s cluster, so long as you have the kubeconfig file.

2. It assumes internet connection to be able to curl the [Aqua official Deployment GitHub repository](https://github.com/aquasecurity/deployments/tree/2022.4) directly to do the corresponding applies.
    1. Due to using the deployments directly, it assumes that the Aqua images are pulled from the official Aqua private registry. See the Aqua registry secret stage.

3. It runs using the GitHub Action generic runner environment, aka latest ubuntu.
    1. It installs Kubernetes to run kubectl directly

### local_manifests

The features of the local_manifests.yml:

1. The code is cloud-agnostic. It can be used to deploy on any K8s cluster, so long as you have the kubeconfig file.

2. It creates the K8s resources using the manifests from the yamls directory.

3. It runs using the GitHub Action generic runner environment, aka latest ubuntu.
    1. It installs Kubernetes to run kubectl directly

### Secrets & variables

#### Secrets

| Name | Description |
| ---- | ----------- |
| `AQUA_DOCKER_USERNAME` | Docker registry username used to pull Aqua Enforcer images |
| `AQUA_DOCKER_PASSWORD` | Docker registry password used to pull Aqua Enforcer images |
| `AQUA_ENFORCER_TOKEN`  | Token for authenticating the Aqua Enforcer with Aqua Server |
| `AQUA_REG_USERNAME` | Username for authenticating with the registry that stores the Aqua image |
| `AQUA_REG_PASSWORD` | Password for authenticating with the registry that stores the Aqua image |
| `AQUA_SAAS_USER` | Aqua SaaS user that will make the API call |
| `AQUA_SAAS_PASSWORD` | Password of Aqua SaaS users that will make the API call |
| `KUBE_CONFIG_B64` | Base64-encoded Kubernetes configuration file (kubeconfig) for authenticating with the cluster |

#### Variables

| Name | Description |
| ---- | ----------- |
| `PLATFORM`| Specifies the Kubernetes platform (e.g., `eks`, `gke`, `native_k8s`, `openshift`, etc.) for the RBAC manifest |
| `AQUA_CONSOLE_URL` | The Aqua Console URL for making CWPP API calls. Needs to be prepended by https |
| `AQUA_AUTH_URL` | The Aqua URL for SaaS authentication. It could be the same as the console value. Needs to be prepended by https |
| `AQUA_GATEWAY_URL` | The URL of the Aqua Gateway that the Enforcer connects to. Does not need to be prepended by https |
| `AQUA_REG` | The registry that stores the Aqua Enforcer image |
| `AQUA_IMAGE` | The full name of the Aqua Enforcer image (repository path and tag) |

## Notes

Any miscellaneous points or interesting observations can be added here.

## Troubleshooting & debugging

General troubleshooting guide information should be added here.

### Issue 1

If you are encountering grpc or networking errors, check the following:

* Is the network opened?
* Is the port correct?
* In the `AQUA_GATEWAY_URL`, is gw present? i.e. `<console_url>-gw.cloud.aquasec.com:443`

## To-do list

* Support KE deployment
* Possible Workflows:
    1. gke_marketplace_plugin: Use the GHA marketplace deploy to GKE action.
* ~~Support generic repositories~~
    * Rejected. This is dependent on the YAML files and the way the K8s resource is deployed. It will vary according to the workflow

## Glossary

| Acronym | Meaning |
|---------|---------|
| **RBAC** | Role-Based Access Control |
| **K8s** | Kubernetes |
| **SCC** | Security Context Constraints (specific to OpenShift) |
| **CRD** | Custom Resource Definition |
| **CI/CD** | Continuous Integration / Continuous Deployment |
| **GHA** | GitHub Action |

## References

* Original deployment used for reference found [here](https://github.com/aquasecurity/deployments/tree/2022.4/enforcers/aqua_enforcer/kubernetes_and_openshift/manifests).
