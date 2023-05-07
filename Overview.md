
# Kubernetes Course

# Azure Public IPs

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

<img width="594" alt="SCR-20230421-sp" src="https://user-images.githubusercontent.com/54627871/236670442-0d783998-334b-4fd3-b87f-8e8d09b33c1c.png">
<img width="485" alt="SCR-20230421-ym" src="https://user-images.githubusercontent.com/54627871/236670444-4ddc4886-8c05-4059-91bb-36f4600cf751.png">


1. Command : sudo apt-get install condtainerd
2. Automated the task using shell scripting.
3. Installed Kubeadm configurations.
4. Added the WeaveNet CNI (Container Networking Interface) plugin to enable networking in the cluster.
5. Deployed an Nginx pods using a deployment and added service ( IP’s ) to the Pods

<div align=center>
<img width="1067" alt="SCR-20230421-md" src="https://user-images.githubusercontent.com/54627871/236670496-f0688303-a235-499a-bea8-6c4a7ddb44d9.png">
<img width="899" alt="SCR-20230421-l7" src="https://user-images.githubusercontent.com/54627871/236670492-508cc980-d22a-4f9b-9eae-a8d9def97fa9.png">
<img width="826" alt="SCR-20230421-lo" src="https://user-images.githubusercontent.com/54627871/236670494-c0aa9b64-62e5-421c-a5d1-b132d286f68e.png">
</div>

1. Accessing Nginx Server through test pod using service
2. DNS in Kubernetes
3. Configuring the NodePort for accessing server from the Internet - Testing Env
4. Creating load balancer for a the Cluster
5. setting up Ingress using Helm 
6. set the ingress class correctly to access from internet
7. Creating RBAC for groups and user


<img width="526" alt="SCR-20230421-lo" src="https://user-images.githubusercontent.com/54627871/236670559-1205d8f8-e001-4f7e-9b0f-988e4f7ce083.jpeg">


1. Using custom certificates generated to execute command ( other than kube-admin )
