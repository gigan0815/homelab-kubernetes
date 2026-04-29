# Homelab Kubernetes

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
    └── deployments/
        └── nginx/
            ├── deployment.yml
            └── service.yml

## Deployments

### nginx
Simple nginx deployment for learning purposes.

    kubectl apply -f deployments/nginx/deployment.yml
    kubectl apply -f deployments/nginx/service.yml

## Usage

Apply all manifests in a directory:

    kubectl apply -f deployments/nginx/

Check status:

    kubectl get pods
    kubectl get services
