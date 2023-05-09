# Worker Node Setup


The worker nodes are the machines that run your applications. They are the machines that will be running your containers. In this section, we will be setting up the worker nodes for our cluster.

---

## Hardware requirement for cluster node 
1. 2 CPU
2. 2 GB RAM

Ports in the firewall that need to be open for the cluster to work properly in master and worker node:

### Master Node
1. 6443 # Kubernetes API Server
2. 2379-2380 # etcd server client API
3. 10250 # Kubelet API
4. 10257 # kube-scheduler
5. 10259 # kube-controller-manager

<!-- Image Here -->

## Worker Node

1. 10250 # Kubelet API  
2. 30000-32767 # NodePort Services




Kubernetes link : https://kubernetes.io/docs/setup/production-environment/tools/kubeadm/install-kubeadm/

___
The install.sh script installs containerd to the node. 

## Containerd
Containerd is a container runtime other than docker that is used to run containers on the node. It also installs the kubeadm, kubelet, and kubectl packages. These packages are used to manage the Kubernetes cluster.

---

The kubeinstall.sh script installs the kubeadm, kubelet, and kubectl packages. These packages are used to manage the Kubernetes cluster.


## Kubeadm
Kubeadm is a tool that is used to bootstrap the Kubernetes cluster. It is used to initialize the master node and join the worker nodes to the cluster.


## kubectl
kubectl is a command-line tool that is used to manage the Kubernetes cluster. It is used to deploy and manage applications on the cluster.

## kubelet
kubelet is a service that runs on each node in the cluster. It is used to manage the containers running on the node.