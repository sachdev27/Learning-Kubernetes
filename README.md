
# Kubernetes Course

# Azure Public IPs

Master : 20.197.63.120

Node1 : 52.140.113.190

Node2 : 20.193.229.150

![SCR-20230420-w0z.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/cf416125-b559-469e-ace8-7d009dd00214/SCR-20230420-w0z.png)

![SCR-20230420-w1x.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/64a75e93-7cd8-4241-86dc-c6bee3b28ab0/SCR-20230420-w1x.png)

![SCR-20230420-w2v.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/27a14160-5fc9-426d-8058-ad7740d92b0b/SCR-20230420-w2v.png)

![SCR-20230420-w3b.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/2bd8b675-0915-44a0-9aff-6ce4b92fbbe0/SCR-20230420-w3b.png)

Steps

  

1. Deployed Azure Virtual Machine instances with Linux images for the master and worker nodes.
2. Allowed inbound traffic to the master and worker node VMs.
3. Installed the containerd runtime on the nodes.

![SCR-20230421-sp.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/9e309a6a-1e7f-415d-8270-0df724bfb9bf/SCR-20230421-sp.png)

![SCR-20230421-yy.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/a100d244-906b-48a1-8315-bcbb37c1652e/SCR-20230421-yy.png)

1. Command : sudo apt-get install condtainerd
2. Automated the task using shell scripting.
3. Installed Kubeadm configurations.
4. Added the WeaveNet CNI (Container Networking Interface) plugin to enable networking in the cluster.
5. Deployed an Nginx pods using a deployment and added service ( IP’s ) to the Pods

![SCR-20230421-md.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/2205f9d7-3e42-4bcb-b560-f7e8365dd1ae/SCR-20230421-md.png)

![SCR-20230421-l7.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/4e72af55-35fc-4a0c-a304-6d7db29b1e17/SCR-20230421-l7.png)

![SCR-20230421-lo.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/ce60ab38-095d-473e-8d1b-6f312b39e457/SCR-20230421-lo.png)

1. Accessing Nginx Server through test pod using service
2. DNS in Kubernetes
3. Configuring the NodePort for accessing server from the Internet - Testing Env
4. Creating load balancer for a the Cluster
5. setting up Ingress using Helm 
6. set the ingress class correctly to access from internet
7. Creating RBAC for groups and user

![SCR-20230506-u1m.jpeg](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/77e94bae-0d0c-4e4d-9ba6-fe198472b5b0/SCR-20230506-u1m.jpeg)

1. Using custom certificates generated to execute command ( other than kube-admin )
