# homelab-kubernetes

Kubernetes manifests for services running on a 3-node cluster on Proxmox VMs.

For a full overview of the homelab infrastructure see the
[homelab repository](https://github.com/gigan0815/homelab).

## Cluster

| Node | IP | Role | OS |
|------|-----|------|----|
| k8smaster | 192.168.1.80 | control-plane | Ubuntu 24.04 |
| k8sworker1 | 192.168.1.81 | worker | Ubuntu 24.04 |
| k8sworker2 | 192.168.1.82 | worker | Ubuntu 24.04 |

## Repository Structure

    homelab-kubernetes/
    ├── .github/
    │   └── workflows/
    │       └── k8s-validate.yml
    ├── deployments/
    │   └── nginx/
    │       ├── configmap.yml
    │       ├── deployment.yml
    │       ├── secret.yml
    │       └── service.yml
    ├── helm/
    │   └── nginx/
    │       └── values.yml
    ├── docs/
    │   └── kubectl-cheatsheet.md
    └── README.md

## Deployments

### nginx
Simple nginx deployment for learning purposes. Uses a ConfigMap for the
HTML content and a Secret for environment variables.

    kubectl apply -f deployments/nginx/

## Helm

Helm chart values for nginx using the bitnami chart.

    helm install my-nginx bitnami/nginx --namespace helm-test -f helm/nginx/values.yml

## CI/CD

Automated YAML manifest validation runs on every push to main via GitHub Actions.
The self-hosted runner is deployed on the github-runner LXC container.

### Workflows
- `k8s-validate.yml` - validates all Kubernetes manifests using kubeconform

## Usage

Apply all manifests in a directory:

    kubectl apply -f deployments/nginx/

Check status:

    kubectl get pods -n webserver
    kubectl get services -n webserver
