# gha-aqua-agent-deployment

## Description

Github action repository for deploying the Aqua Enforcer.

## Variables & secrets

### Secrets

| Name | Description |
| ---- | ----------- |
| `AQUA_DOCKER_USERNAME` | Docker registry username used to pull Aqua Enforcer images |
| `AQUA_DOCKER_PASSWORD` | Docker registry password used to pull Aqua Enforcer images |
| `AQUA_ENFORCER_TOKEN`  | Token for authenticating the Aqua Enforcer with Aqua Server |
| `KUBE_CONFIG_B64` | Base64-encoded Kubernetes configuration file (kubeconfig) for authenticating with the cluster |

### Variables

| Name | Description |
| ---- | ----------- |
| `PLATFORM`| Specifies the Kubernetes platform (e.g., `eks`, `gke`, `native_k8s`, `openshift`, etc.) for the RBAC manifest |
| `AQUA_GATEWAY_URL` | The URL of the Aqua Gateway that the Enforcer connects to |

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
