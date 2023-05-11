# Volume in Kubernetes



## Persistent Volume

A PersistentVolume (PV) is a piece of storage in the cluster that has been provisioned by an administrator or dynamically provisioned using Storage Classes. It is a resource in the cluster just like a node is a cluster resource. PVs are volume plugins like Volumes, but have a lifecycle independent of any individual pod that uses the PV. This API object captures the details of the implementation of the storage, be that NFS, iSCSI, or a cloud-provider-specific storage system.

The Persistent Volume are available in the cluster and can be used by any pod in the cluster and in any namespace.

```yaml
apiVersion: v1
kind: PersistentVolume
metadata:
  name: pv-volume
spec:
    storageClassName: manual
    capacity:
        storage: 10Gi
    accessModes:
        - ReadWriteOnce
    hostPath:
        path: "/mnt/data" # directory on host machine 
```

## Persistent Volume Claim

A PersistentVolumeClaim (PVC) is a request for storage by a user. It is similar to a pod. Pods consume node resources and PVCs consume PV resources. Pods can request specific levels of resources (CPU and Memory). Claims can request specific size and access modes (e.g., can be mounted once read/write or many times read-only).

```yaml 
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: pv-claim
spec:
    accessModes:
        - ReadWriteOnce
    resources:
        requests:
            storage: 3Gi
```

## Storage Class

A StorageClass provides a way for administrators to describe the "classes" of storage they offer. Different classes might map to quality-of-service levels, or to backup policies, or to arbitrary policies determined by the cluster administrators. Kubernetes itself is unopinionated about what classes represent. This concept is sometimes called "profiles" in other storage systems.

```yaml
apiVersion: storage.k8s.io/v1
kind: StorageClass
metadata:
  name: manual
provisioner: kubernetes.io/host-path
volumeBindingMode: WaitForFirstConsumer
```


### Config Map and Secrets in Volume

ConfigMaps and Secrets are volumes that can be mounted to a pod. They are used to store configuration data and sensitive information such as passwords, API keys, and other secrets. They are stored in the etcd database and can be accessed by any pod in the cluster.

These volumes are mounted to a pod using the same syntax as other volumes, but they are not created by the pod itself. Instead, they are created by the Kubernetes API server when the pod is created. This means that the pod does not need to be restarted when the ConfigMap or Secret is updated.



## Sharing Volume between containers

There are cases where we need to share the volume between two containers in the same pod. This can be done by using the same volume name in both the containers. 
Example: Log files of the application can be shared with the logstash container to send the logs to the ELK (Elasticsearch, Logstash, Kibana) stack.

### EmptyDir

EmptyDir is used to create a temporary directory on the host machine and share it between the containers. The data in the directory is deleted when the pod is deleted.

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: two-containers
spec:
    volumes:
        - name: shared-data
        emptyDir: {}
    containers:
        - name: nginx-container
        image: nginx
        volumeMounts:
            - name: shared-data
            mountPath: /usr/share/nginx/html
        - name: debian-container
        image: debian
        volumeMounts:
            - name: shared-data
            mountPath: /pod-data
        command: ["/bin/sh"]
        args: ["-c", "echo Hello from the debian container > /pod-data/index.html"]
```






