# Liveness and Readiness probe

## Liveness probe

Liveness probe is used to check if the container is still alive. If the liveness probe fails, the container will be restarted.

### Example: Liveness probe

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: liveness-pod
spec:
    containers:
    - name: liveness-container
        image: nginx
        livenessProbe:
            httpGet:
                path: /
                port: 80
            initialDelaySeconds: 15
            periodSeconds: 5
        # Liveness using TCP Socket
        livenessProbe:
            tcpSocket:
                port: 8080
            initialDelaySeconds: 15
            periodSeconds: 5
        # Liveness using Exec
        livenessProbe:
            exec:
                command:
                - cat
                - /tmp/healthy
            initialDelaySeconds: 15
            periodSeconds: 5
```

## Readiness probe

Readiness probe is used to check if the container is ready to receive traffic. If the readiness probe fails, the container will not receive any traffic.

### Example: Readiness probe

```yaml

apiVersion: v1
kind: Pod
metadata:
  name: readiness-pod
spec:
    containers:
    - name: readiness-container
        image: nginx
        readinessProbe:
            httpGet:
                path: /
                port: 80
            initialDelaySeconds: 15
            periodSeconds: 5 
```