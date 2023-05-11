# Configmap and Secrets


Pods can consume ConfigMap and Secrets in two different ways:

1. As individual values using Environment Variables
2. As config files using Volume Mounts


## ConfigMap

ConfigMap is a Kubernetes API object that provides a way to inject configuration data into Pods. It can be used to store configuration data such as database connection strings, API keys, and other configuration details.

ConfigMap is a key-value pair that can be used to store configuration data. It can be used to store configuration data such as database connection strings, API keys, and other configuration details.

```bash
kubectl create configmap <configmap-name> --from-literal=<key>=<value>
```

```yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: app-config
data:
    app-color: blue
    app-size: large
```
    

## Secrets

Secrets are similar to ConfigMaps, but they are used to store sensitive information such as passwords, API keys, and other sensitive data. Secrets are stored in the cluster and can be accessed by Pods using environment variables or volume mounts.

```bash
kubectl create secret generic <secret-name> --from-literal=<key>=<value>
```

```yaml
apiVersion: v1
kind: Secret
metadata:
  name: app-secret
type: Opaque # type of secret
data:
    app-password: cGFzc3dvcmQ= # base64 encoded password
```
### Types of secret

There are Builtin types of secrets in Kubernetes:
1. Opaque: This is the default type of secret. It is used to store arbitrary data. It is encoded using base64 encoding.
2. kubernetes.io/service-account-token: This type of secret is used to store the service account token for a pod. It is used to authenticate the pod to the Kubernetes API server.
3. kubernetes.io/dockerconfigjson: This type of secret is used to store the Docker credentials for a pod. It is used to authenticate the pod to the Docker registry.
4. kubernetes.io/dockercfg: This type of secret is used to store the Docker credentials for a pod. It is used to authenticate the pod to the Docker registry.


## Using ConfigMap and Secrets in Pods

ConfigMap and Secrets can be used in Pods using environment variables or volume mounts.

### Environment Variables

ConfigMap and Secrets can be used in Pods using environment variables. The following example shows how to use ConfigMap and Secrets in Pods using environment variables:

```yaml

apiVersion: v1
kind: Pod
metadata:
  name: app-pod
spec:
    containers:
    - name: app-container
        image: nginx
        env:
        - name: APP_COLOR
        valueFrom:
            configMapKeyRef:
            name: app-config
            key: app-color
        - name: APP_SIZE
        valueFrom:
            configMapKeyRef:
            name: app-config
            key: app-size
        - name: APP_PASSWORD
        valueFrom:
            secretKeyRef:
            name: app-secret
            key: app-password
```


### Volume Mounts

ConfigMap and Secrets can be used in Pods using volume mounts. The following example shows how to use ConfigMap and Secrets in Pods using volume mounts:

```yaml

apiVersion: v1
kind: Pod
metadata:
  name: app-pod
spec:
    volumes:
    - name: app-config-volume # volume name
        configMap: 
        name: app-config # configmap name
    - name: app-secret-volume # volume name
        secret:
        name: app-secret # secret name
    containers:
    - name: app-container
        image: nginx
        volumeMounts:
        - name: app-config-volume # volume name
        mountPath: /etc/config
        readOnly: true
        - name: app-secret-volume # volume name
        mountPath: /etc/secret
        readOnly: true
```

### ConfigMap for volume mount

```yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: app-config
data:
    app.conf:
    | server {
    |     listen 80;
    |     server_name localhost;
    |     location / {
    |         root /usr/share/nginx/html;
    |         index index.html;
    |     }
    | }
```


## Restarting the Pod for applying the changes


```bash
kubectl delete pod <pod-name>
```

### Rollout Restarting for restart deployment

```bash
kubectl rollout restart deployment <deployment-name>
```
