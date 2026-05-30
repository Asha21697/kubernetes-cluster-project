# Kubernetes Multi-Node Cluster Setup, Troubleshooting and Nginx Deployment 

## Project Overview

This project demonstrates the setup, troubleshooting, and validation of a Kubernetes multi-node cluster consisting of 1 Master Node and 3 Worker Nodes using kubeadm, containerd, and Calico networking.

The project includes cluster initialization, worker node joining, troubleshooting of real-world Kubernetes issues, and deployment of an Nginx application using Kubernetes Deployments and Services.

- 1 Master Node
- 3 Worker Nodes

After creating the cluster, an Nginx application was deployed using Kubernetes Deployment and Service resources.

## Environment

- Operating System: Ubuntu Linux
- Virtualization Platform: VMware Workstation
- Kubernetes
- kubeadm
- kubelet
- kubectl
- Containerd 
- Calico CNI
- YAML


## Cluster Architecture

```
Master Node
│
├── Worker Node 1
├── Worker Node 2
└── Worker Node 3
```

## Objectives

- Create a multi-node Kubernetes cluster.
- Join worker nodes to the master node.
- Deploy containerized applications.
- Expose applications using Kubernetes Services.
- Manage pods and deployments using kubectl.

## Installation Steps

### Initialize Kubernetes Master Node

```bash
sudo kubeadm init
```

### Configure kubectl

```bash
mkdir -p $HOME/.kube
sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
sudo chown $(id -u):$(id -g) $HOME/.kube/config
```

Generate Join Command
kubeadm token create --print-join-command


### Join Worker Nodes

```bash
kubeadm join <MASTER-IP>:6443 --token <TOKEN> \
--discovery-token-ca-cert-hash sha256:<HASH>
```

### Verify Cluster

```bash
kubectl get nodes
```

## Nginx Deployment

### Create Deployment

```bash
kubectl create deployment nginx-deploy --image=nginx --replicas=3
```

### Verify Pods

```bash
kubectl get pods -o wide
```

### Create Expose Service

```bash
kubectl expose deployment nginx-deploy --type=NodePort --port=80
```

### Verify Services

```bash
kubectl get svc 
```

Additional Resources

YAML manifests (deployment.yaml and service.yaml) are also included in this repository for Kubernetes resource management and deployment automation.

## Project Files

```
kubernetes-cluster-project/
│
├── deployment.yaml
├── service.yaml
├── README.md
├── commands.md
├── kubernetes_cluster_journey.pdf
├── kubernetes_cluster_troubleshooting_journey.pdf
│
└── screenshots/
    ├── cluster-ready.png
    ├── nodes-output.png
    ├── get-pods.png
    ├── get-services.png
    └── nginx-working.png
```

## Screenshots

### Cluster Ready

![Cluster Ready](screenshots/cluster-ready.png)

### Nodes Output

![Nodes Output](screenshots/nodes-output.png)

### Pods Running

![Pods Running](screenshots/get-pods.png)

### Services Running

![Services Running](screenshots/get-services.png)

### Nginx Application

![Nginx Application](screenshots/nginx-working.png)

## Commands Used
Note: Both YAML-based deployment and kubectl CLI deployment methods were practiced during the project.

```bash
kubectl get nodes
kubectl get pods
kubectl get svc

kubectl apply -f deployment.yaml
kubectl apply -f service.yaml

kubectl create deployment nginx-deploy --image=nginx --replicas=3
kubectl expose deployment nginx-deploy --type=NodePort --port=80

kubeadm token create --print-join-command 
```

## Project Highlights

- Kubernetes Cluster Setup - Built a multi-node Kubernetes cluster with 1 Master Node and 3 Worker Nodes.
- Container Runtime Configuration - Configured containerd as the container runtime.
- Calico Networking - Installed and configured Calico CNI for cluster networking.
- Worker Node Integration - Joined worker nodes using kubeadm.
- Cluster Troubleshooting - Diagnosed and resolved worker node join failures.
- kubelet Issue Resolution - Fixed kubelet configuration and startup issues.
- Token Discovery Fixes - Resolved JWS signature and token discovery errors.
- Application Deployment - Deployed Nginx using Kubernetes Deployment.
- Service Exposure - Exposed the application through a NodePort Service.
- Cluster Validation - Verified cluster health, networking, and service accessibility.

## Skills Demonstrated

- Linux Administration - System management and troubleshooting
- Kubernetes Administration - Cluster deployment and management
- kubeadm Cluster Setup - Multi-node cluster initialization
- Worker Node Management - Node joining and maintenance
- containerd Runtime Configuration - Container runtime setup
- Calico Networking - Kubernetes network configuration
- Cluster Troubleshooting - Issue diagnosis and resolution
- Deployment Management - Application deployment handling
- NodePort Services - Service exposure and access management
- YAML Configuration - Kubernetes resource definitions
- Kubernetes Networking - Cluster communication setup
- System Debugging - Error analysis and troubleshooting

## Key Learning Outcomes

- Kubernetes Architecture - Understanding cluster components and overall architecture
- Control Plane and Worker Node Communication - Managing communication between cluster nodes
- kubeadm Cluster Lifecycle Management - Cluster initialization, joining, and maintenance
- Container Runtime Integration - Working with containerd as the container runtime
- Calico Networking - Configuring and troubleshooting Kubernetes networking
- kubelet Troubleshooting - Diagnosing and resolving kubelet-related issues
- Token Discovery Mechanism - Understanding node authentication and cluster joining
- Deployment and Service Management - Managing applications using Deployments and Services
- Kubernetes Debugging Techniques - Identifying and resolving cluster issues effectively


## Troubleshooting Experience

During the Kubernetes cluster setup, several real-world issues were encountered and resolved:

### Worker Node Join Failure

* kubeadm join became stuck during the discovery phase.
* Generated a fresh join token from the master node.
* Rejoined worker nodes successfully.

### kubelet Configuration Issues

* Worker nodes failed to load kubelet configuration files.
* Cleaned old Kubernetes state and reconfigured nodes.
* Restarted kubelet and containerd services.

### JWS Signature / Discovery Token Error

* Encountered cluster-info ConfigMap discovery errors.
* Regenerated join tokens and repeated the join process.
* Successfully synchronized worker nodes with the control plane.

### Calico Networking Initialization

* Calico pods remained in PodInitializing state.
* Verified pod status and networking configuration.
* Confirmed successful transition to Running state.

### Cluster Validation

Successfully verified:

* Master Node Ready
* Worker Node 1 Ready
* Worker Node 2 Ready
* Worker Node 3 Ready

---

## Future Enhancements

* Helm Package Management
* Ingress Controller
* Persistent Volumes
* RBAC Configuration
* Prometheus Monitoring
* Grafana Dashboards
* Jenkins CI/CD Pipeline
* Horizontal Pod Autoscaling

## Author

   Asha
