# RBAC ( Role Based Access Control )

## Table of Contents
1. [RBAC Authentication](#rbac-authentication)
2. [RBAC Authorization](#rbac-authorization)


##  RBAC Authentication

1. Creating RSA Client key for user using openssl
```bash
openssl genrsa -out <username>.key 2048
```

2. Creating a CSR for the user 
```bash
openssl req -new -key <username>.key -out <username>.csr -subj "/CN=<username>/O=<group>"
```
3. Approving the CSR for the user
```bash
kubectl certificate approve <username>
```

## RBAC Authorization

1. Creating a Role for the user
```bash
kubectl create role <role-name> --resource=<resource> --verb=<verb>
```
2. Creating a RoleBinding for the user
```bash
kubectl create rolebinding <role-binding-name> --role=<role-name> --user=<username>
```
3. Creating a ClusterRole for the user
```bash
kubectl create clusterrole <cluster-role-name> --resource=<resource> --verb=<verb>
```
4. Creating a ClusterRoleBinding for the user
```bash
kubectl create clusterrolebinding <cluster-role-binding-name> --clusterrole=<cluster-role-name> --user=<username>
```