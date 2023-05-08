# Troubleshooting Guide

## Table of Contents
1. [Troubleshooting in kubernetes](#troubleshooting-in-kubernetes)
2. [Using exec command to access pod](#using-exec-command-to-access-pod)
3. [JSON path queries](#json-path-queries)
4. [creating custom scripts of jsonpath](#creating-custom-scripts-of-jsonpath)
5. [costum column in kubectl](#costum-column-in-kubectl)
6. [Troubleshooting Nodes ](#troubleshooting-nodes)
7. [Kube API Troubleshooting](#kube-api-troubleshooting)



## Troubleshooting in kubernetes

1. is pod running ?
2. is pod registered with service ?
3. is service forwarding request?
4. k get ep (end point)
5. is service accessible ?
6. check logs of pod for container logs
7. check pod status using describe

## Using exec command to access pod

1. k exec -it podname -- sh
2. k exec -it podname -- bash
3. k exec -it nginx -- cat /etc/nginx/nginx.conf
4. k exec -it nginx  -c nginx -- cat /etc/nginx/nginx.conf

## JSON path queries

1. k get pods -o jsonpath='{.items[*].metadata.name}' # all pods
2. k get pod -o jsonpath='{range .items[*]}{.metadata.name}{"\n"}{end}' # new line
3. k get pod -o jsonpath='{range .items[*]}{.metadata.name}{"\t"}{.status.podIP}{"\n"}{end}' # tab separated
4. k get pod -o jsonpath='{range .items[*]}{.metadata.name}{"\t"}{.status.podIP}{"\t"}{.status.startTime}{"\n"}{end}' # tab separated with start time

## creating custom scripts of jsonpath

1. creating a script 
```bash
 kubectl get pods -o jsonpath='{range .items[*]}{.metadata.name}{"\t"}{.status.podIP}{"\t"}{.status.startTime}{"\n"}{end}' > podlist.sh
```

2. giving permission to execute the script
```bash
chmod +x podlist.sh
```

### costum column in kubectl

```bash
kubectl get pods -o custom-columns=POD_NAME:.metadata.name,POD_IP:.status.podIP,START_TIME:.status.startTime
```

## Troubleshooting Nodes 

1. ssh into the node
```bash
ssh -i ~/.ssh/id_rsa azureuser@<ip>
```
2. check the logs of kubelet
```bash
 journalctl -u kubelet
```
```bash
 service kubelet status # check the status of kubelet
 ```
3. check the logs of kube-proxy
```bash
 journalctl -u kube-proxy
```
```bash
 service kube-proxy status # check the status of kube-proxy
 ```
4. check the logs of container runtime
```bash
 journalctl -u docker
```
```bash
 service docker status # check the status of docker
 ```
5. check the logs of kube-apiserver
```bash
 journalctl -u kube-apiserver
```
```bash
 service kube-apiserver status # check the status of kube-apiserver
 ```
6. check the logs of kube-controller-manager
```bash
 journalctl -u kube-controller-manager
```
```bash
 service kube-controller-manager status # check the status of kube-controller-manager
 ```
7.  check the logs of kube-scheduler
```bash
 journalctl -u kube-scheduler
```
```bash
 service kube-scheduler status # check the status of kube-scheduler
 ```
8. check the logs of etcd
```bash
 journalctl -u etcd
```
```bash
 service etcd status # check the status of etcd
 ```
9. check the logs of kube-dns
```bash
 journalctl -u kube-dns
```
```bash
 service kube-dns status # check the status of kube-dns
 ```


## Kube API Troubleshooting

1. Check Kube Config file
```bash
cat ~/.kube/config
```
2. check the CA certificate data in the config file, decode it with base64
```bash
echo <base64 encoded data> | base64 -d
```
and check it with cluster Certificate Authority Data
```bash
cat /etc/kubernetes/pki/ca.crt
```
3. Check the server endpoint in the config file
```bash
cat ~/.kube/config
```
and check it with the server endpoint
```bash
cat /etc/kubernetes/manifests/kube-apiserver.yaml
```

