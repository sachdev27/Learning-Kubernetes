## Deployments and Services



<div align=center>
<img width="1067" alt="SCR-20230421-md" src="https://user-images.githubusercontent.com/54627871/236670496-f0688303-a235-499a-bea8-6c4a7ddb44d9.png">
<img width="899" alt="SCR-20230421-l7" src="https://user-images.githubusercontent.com/54627871/236670492-508cc980-d22a-4f9b-9eae-a8d9def97fa9.png">
<img width="826" alt="SCR-20230421-lo" src="https://user-images.githubusercontent.com/54627871/236670494-c0aa9b64-62e5-421c-a5d1-b132d286f68e.png">
</div>

## ConfigMaps and Secrets

1. Accessing Nginx Server through test pod using service
2. DNS in Kubernetes
3. Configuring the NodePort for accessing server from the Internet - Testing Env
4. Creating load balancer for a the Cluster
5. setting up Ingress using Helm 
6. set the ingress class correctly to access from internet
7. Creating RBAC for groups and user


##  RBAC Authentication

1. Creating RSA Client key for user using openssl
2. Creating a CSR for the user 
3. Approving the CSR for the user

## RBAC Authorization

1. Creating a Role for the user
2. Creating a RoleBinding for the user
3. Creating a ClusterRole for the user
4. Creating a ClusterRoleBinding for the user



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

## JSON path queries

1. k get pods -o jsonpath='{.items[*].spec.containers[*].image}'
2. k get pods -o jsonpath='{.items[*].metadata.name}'