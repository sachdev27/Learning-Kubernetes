# Multiple Container in Pod 


## Table of Contents

1. [Multi Container Pods](#multi-container-pods)
2. [SideCar Container](#sidecar-container)
3. [Init Container](#init-container)


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

