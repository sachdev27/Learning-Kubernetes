# Securing the Cluster


## Network policies in Kubernetes

Description: Network policies in kubernetes are used to control the traffic flow between pods in a cluster. Network policies are implemented using the network policy API. The network policy API is implemented using the network policy controller. The network policy controller is responsible for implementing the network policies in the cluster.

### Implementing a network policy for weavenet CNI

The following command can be used to create a network policy for weavenet CNI:

```bash
kubectl create -f network-policy.yaml
```

```yaml
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: allow-nginx
  namespace: default # namespace
spec:
    podSelector:
        matchLabels:
        app: nginx
    policy types: Ingress # policy type
    ingress:
    - from:
        - podSelector:
            matchLabels:
            app: nginx
        - namespaceSelector: # namespace selector
            matchLabels:
            name: default
        ports:
        - protocol: TCP
        port: 80
```

```yaml 
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: allow-nginx
  namespace: default # namespace
spec:
    podSelector:
        matchLabels:
        app: nginx
    policy types: Egress # policy type
    - to:
        - podSelector:
            matchLabels:
            app: mysql
        - namespaceSelector: # namespace selector
            matchLabels:
            name: default
        ports:
        - protocol: TCP
        port: 3306
```


## Combining the Network policies

Network policies can be combined to create complex network policies. The following example shows how to combine the network policies created in the previous examples:

```yaml
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: allow-nginx
  namespace: default # namespace
spec:
    podSelector:
        matchLabels:
        app: nginx
    policy types: Ingress # policy type
    ingress:
    - from:
        - podSelector:
            matchLabels:
            app: nginx
        - namespaceSelector: # namespace selector
            matchLabels:
            name: default
        ports:
        - protocol: TCP
        port: 80
    - to:
        - podSelector:
            matchLabels:
            app: mysql
        - namespaceSelector: # namespace selector
            matchLabels:
            name: default
        ports:
        - protocol: TCP
        port: 3306
```