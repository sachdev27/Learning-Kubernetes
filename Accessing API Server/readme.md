# API  server

For accessing Kubernetes API server, we need to have a valid certificate and key. The certificate and key are stored in the /etc/kubernetes/pki/apiserver.crt and /etc/kubernetes/pki/apiserver.key files respectively.

We will be creating a Service account for accessing the Kubernetes API server. The Service account will be used to authenticate the user to the Kubernetes API server.

and then we will be creating a cluster role binding for the service account. The cluster role binding will be used to bind the service account to the cluster role.

The cluster role binding will be used to bind the service account to the cluster role.

