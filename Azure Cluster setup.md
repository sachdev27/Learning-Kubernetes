
# Kubernetes Course

## Azure Public IPs

Master : 20.197.XX.XXX

Node1 : 52.140.XX.XXX

Node2 : 20.193.XX.XXX

<div align=center> 
<img width="1008" alt="SCR-20230420-w0z" src="https://user-images.githubusercontent.com/54627871/236670331-d2449c99-7537-4f89-b1ce-1ddb2efe1e0a.png">
<img width="739" alt="SCR-20230420-w3b" src="https://user-images.githubusercontent.com/54627871/236670340-a09f2ba0-03d7-4b83-b5ee-5af0581ce556.png">
</div>

Steps

  

1. Deployed Azure Virtual Machine instances with Linux images for the master and worker nodes. 
2. Allowed inbound traffic to the master and worker node VMs.
3. Installed the containerd runtime on the nodes.
```bash
sudo apt-get update && sudo apt-get install -y containerd
```


<img width="594" alt="SCR-20230421-sp" src="https://user-images.githubusercontent.com/54627871/236670442-0d783998-334b-4fd3-b87f-8e8d09b33c1c.png">
<img width="485" alt="SCR-20230421-ym" src="https://user-images.githubusercontent.com/54627871/236670444-4ddc4886-8c05-4059-91bb-36f4600cf751.png">


4. Installed the kubeadm, kubelet, and kubectl packages on the nodes.
```bash
sudo apt-get update && sudo apt-get install -y apt-transport-https curl
curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key add -
sudo apt-add-repository "deb http://apt.kubernetes.io/ kubernetes-xenial main"
sudo apt-get update
sudo apt-get install -y kubelet kubeadm kubectl
```

5. Initialized the master node using the kubeadm init command.
```bash
sudo kubeadm init --pod-network-cidr= 
```

6. Joined the worker nodes to the cluster using the kubeadm join command.
```bash
sudo kubeadm join
```
7. Installed the WeaveNet network plugin on the cluster.
```bash
kubectl apply -f "https://cloud.weave.works/k8s/net?k8s-version=$(kubectl version | base64 | tr -d '\n')"
```

8. Verified the cluster using the kubectl get nodes command.
```bash
kubectl get nodes
```
