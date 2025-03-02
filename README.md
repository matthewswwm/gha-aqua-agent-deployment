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

#### Secrets

| Name | Description |
| ---- | ----------- |
| `AQUA_DOCKER_USERNAME` | Docker registry username used to pull Aqua Enforcer images |
| `AQUA_DOCKER_PASSWORD` | Docker registry password used to pull Aqua Enforcer images |
| `AQUA_ENFORCER_TOKEN`  | Token for authenticating the Aqua Enforcer with Aqua Server |
| `KUBE_CONFIG_B64` | Base64-encoded Kubernetes configuration file (kubeconfig) for authenticating with the cluster |

#### Variables

| Name | Description |
| ---- | ----------- |
| `PLATFORM`| Specifies the Kubernetes platform (e.g., `eks`, `gke`, `native_k8s`, `openshift`, etc.) for the RBAC manifest |
| `AQUA_GATEWAY_URL` | The URL of the Aqua Gateway that the Enforcer connects to |

## Notes

Any miscellaneous points or interesting observations can be added here.

## Troubleshooting & debugging

General troubleshooting guide information should be added here.

### Issue 1

Info and solutions (if any) for specific issues should have their own dedicated section.

## To-do list

* Support KE deployment
* Possible Workflows:
    1. generic_self_maintained:
        1. Store the YAML files in this repo
        2. Clone the repo
        3. Apply the files
        4. Don't need to curl the official deployment repository
    2. gke_marketplace_plugin: Use the GHA marketplace deploy to GKE action.
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
