# Proxy Setup 


We can access the kubectl command from the master node. But we can't access the kubectl command from the worker node. To access the kubectl command from the worker node, we need to set up a proxy server on the master node. The proxy server will forward the requests from the worker node to the master node.

## Steps

1. Create a proxy server on the master node using the kubectl proxy command.

```bash
kubectl proxy --address=' <master-node-ip> ' --port=8080 --accept-hosts='^*$'
```

### stoppping the proxy server by killing the process

```bash
ps -ef | grep kubectl
```

```bash
kill -9 <process-id>
```


## Accessing the proxy server from the worker node

1. Get the IP address of the master node.

```bash
kubectl get nodes -o wide
```

2. Get the port number of the proxy server.

```bash
kubectl get svc
```

3. Access the proxy server from the worker node using the IP address and port number of the master node.

```bash
curl http://<master-node-ip>:<port-number>/api/v1/namespaces/default/pods
```

## using certificate and Authorization tokens to access the proxy server


```bash
curl -X get http://<master-node-ip>:<port-number>/api/v1/namespaces/default/pods --header "Bearer: <authorization-token>" --ca-cert <certificate>
``` 
