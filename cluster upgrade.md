# Cluster upgrade

## Upgrade the cluster

1. Upgrade the control plane nodes first
2. Upgrade the worker nodes
3. Upgrade the kubelet and kubectl packages on the control plane nodes
4. Upgrade the kubelet and kubectl packages on the worker nodes

## Upgrade the control plane nodes

1. Drain the control plane node
```bash
kubectl drain <control-plane-node-name> --ignore-daemonsets
```

2. Upgrade the control plane node
```bash
apt-get update && apt-get upgrade -y
```

3. Uncordon the control plane node
```bash
kubectl uncordon <control-plane-node-name>
```

## Upgrade the worker nodes

1. Drain the worker node
```bash
kubectl drain <worker-node-name> --ignore-daemonsets
```

2. Upgrade the worker node
```bash
apt-get update && apt-get upgrade -y
```

3. Uncordon the worker node
```bash
kubectl uncordon <worker-node-name>
```

## Upgrade the kubelet and kubectl packages on the control plane nodes

1. Drain the control plane node
```bash
kubectl drain <control-plane-node-name> --ignore-daemonsets
```

2. Upgrade the kubelet and kubectl packages on the control plane node
```bash
apt-get update && apt-get install -y kubelet kubeadm kubectl
```

3. Uncordon the control plane node
```bash
kubectl uncordon <control-plane-node-name>
```

## Upgrade the kubelet and kubectl packages on the worker nodes

1. Drain the worker node
```bash
kubectl drain <worker-node-name> --ignore-daemonsets
```

2. Upgrade the kubelet and kubectl packages on the worker node
```bash
apt-get update && apt-get install -y kubelet kubeadm kubectl
```

3. Uncordon the worker node
```bash

kubectl uncordon <worker-node-name>
```


