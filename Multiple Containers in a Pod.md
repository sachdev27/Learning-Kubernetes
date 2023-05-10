# Multiple Container in Pod 


## Table of Contents

1. [Multi Container Pods](#multi-container-pods)
2. [SideCar Container](#sidecar-container)
3. [Init Container](#init-container)
4. [Exposing Pod Information to the Containers](#exposing-pod-information-to-the-containers)
5. [Exposing Pod Information to the Containers using Volume Mounts](#exposing-pod-information-to-the-containers-using-volume-mounts)



## Multi Container Pods

Description: A pod can have multiple containers running inside it. These containers share the same resources and network. They can communicate with each other using localhost. They are used to run helper containers alongside the main container in the pod. For example, a pod can have a main container running an application and a sidecar container running a logging agent.


## SideCar Container

Description: Sidecar containers are helper containers that run alongside the main container in a pod. They are used to provide additional functionality to the main container in the pod. For example, a sidecar container can be used to provide logging, monitoring, or additional security to the main container in the pod.

### Example: Sidecar Container

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: sidecar-pod
spec:
    containers:
    - name: main-container
        image: nginx
    - name: sidecar-container
        image: busybox
        command: ['sh', '-c', 'echo Hello from the sidecar container! && sleep 3600']
```


## Init Container

Description: Init containers are used to perform initialization logic before the main container in a pod is started. They are used to perform tasks such as database migrations, downloading assets, or running tests. Init containers are run to completion before the main container is started. If an init container fails, the pod restarts until the init container succeeds.

### Example: Init Container

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: init-container-pod
spec:
    containers:
    - name: main-container
        image: nginx
    initContainers:
    - name: init-container
        image: busybox
        command: ['sh', '-c', 'echo Hello from the init container! && sleep 3600']

```



## Exposing Pod Information to the Containers

Description: Containers running in a pod can access information about the pod using environment variables and Volume mounts. This information can be used to configure the containers running in the pod

The environment variables are automatically created by Kubernetes and are available to the containers running in the pod. The following environment variables are available to the containers running in a pod:

- POD_NAME: The name of the pod.
- POD_NAMESPACE: The namespace of the pod.
- POD_IP: The IP address of the pod.
- POD_SERVICE_ACCOUNT: The service account associated with the pod.
- POD_NODE_NAME: The name of the node that the pod is running on.
- POD_UID: The UID of the pod.
- POD_RESTARTS: The number of times the pod has been restarted.
- POD_HOST_IP: The IP address of the node that the pod is running on.
- POD_HOSTNAME: The hostname of the node that the pod is running on.
- POD_IPS: The IP addresses of the pod.
- POD_IPS_<CONTAINER_NAME>: The IP addresses of the containers in the pod.

### Example: Exposing Pod Information to the Containers

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: pod-info-pod
spec:
    containers:
    - name: main-container
        image: nginx
        env:
        - name: POD_NAME
            valueFrom:
              fieldRef:
                fieldPath: metadata.name
        - name: POD_SERVICE_ACCOUNT
            valueFrom:
              fieldRef:
                fieldPath: spec.serviceAccountName
        - name: POD_IP
            valueFrom:
              fieldRef:
                fieldPath: status.podIP
```

## Exposing Pod Information to the Containers using Volume Mounts

Example: 

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: pod-info-pod
spec:
    containers:
    - name: main-container
        image: nginx
        volumeMounts:
        - name: pod-info
            mountPath: /etc/pod-info
    volumes:
    - name: pod-info
        downwardAPI:
        items:
        - path: "name"
            fieldRef:
            fieldPath: metadata.name
        - path: "namespace"
            fieldRef:
            fieldPath: metadata.namespace
        - path: "podIP"
            fieldRef:
            fieldPath: status.podIP
```