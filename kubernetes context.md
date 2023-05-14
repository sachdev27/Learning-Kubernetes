# Cluster Context 


Description: A cluster context is a set of configuration parameters that define how to connect to a Kubernetes cluster. A cluster context is used to connect to a Kubernetes cluster using the kubectl command line tool.


An administrator can create multiple cluster contexts for a single Kubernetes cluster. This allows the administrator to connect to the cluster using different configurations.

Multiple cluster contexts can be created using the kubectl config command. The following command can be used to create a cluster context:

```bash
kubectl config set-cluster <cluster-name> --server=<server-url> --certificate-authority=<ca-file-path> --embed-certs=true
```

### The following command can be used to view the list of cluster contexts:

```bash
kubectl config get-clusters
```

### changing the context

```bash
kubectl config use-context <context-name>
```

