# Rollout Plan and strategy


Kubernetes provides several deployment strategies that can be used to update or roll out a new version of an application. The different deployment strategies are designed to provide different levels of control over the rollout process, and they have different trade-offs between deployment speed and risk. Here are some of the most commonly used deployment strategies in Kubernetes:

Rolling Update:
Rolling update is the default deployment strategy in Kubernetes. It updates pods in a rolling fashion, meaning that only a subset of pods are updated at a time, while the remaining pods continue to serve traffic. This approach ensures that the application remains available during the update process and minimizes downtime.

ReCreate:
Recreate is a deployment strategy that deletes all pods before creating new ones. This approach is useful when you want to ensure that all pods are running the same version of the application. However, it can result in downtime if the application is not designed to handle this type of deployment.


## Configuration in Deployment yaml file

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
spec:
    replicas: 3 # number of pods
    selector:
        matchLabels:
        app: nginx
    strategies: # deployment strategy
        type: RollingUpdate
        rollingUpdate:
        maxSurge: 1 # maximum number of pods that can be created above the desired number of pods
        maxUnavailable: 1 # maximum number of pods that can be unavailable during the update process
    template:
        metadata:
        labels:
            app: nginx
        spec:
        containers: # container details
        - name: nginx
            image: nginx:1.14.2
            ports:
            - containerPort: 80
``` 


In this example, the Deployment object specifies a RollingUpdate deployment strategy, with the following configuration options:

- maxUnavailable: This field specifies the maximum number of pods that can be unavailable during the update process. In this case, only one pod can be unavailable at any given time.
- maxSurge: This field specifies the maximum number of pods that can be created above the desired number of replicas during the update process. In this case, only one additional pod can be created at any given time.



## Rollout history

Kubernetes keeps track of the rollout history of a deployment. This allows you to view the history of a deployment and roll back to a previous version if necessary. The rollout history is stored in the annotations of the Deployment object. The following command can be used to view the rollout history of a deployment:

```bash
kubectl rollout history deployment nginx-deployment
```

```bash
kubectl rollout history deployment nginx-deployment --revision=2
```

Rollout history can be useful for debugging and troubleshooting deployment issues, as well as for keeping track of changes made to the application and configuration over time. You can also use the kubectl rollout undo command to roll back to a previous revision of the Deployment object if necessary.


## Rollout undo

Kubernetes provides a rollback feature that allows you to roll back to a previous revision of a Deployment object. This can be useful if you need to revert a change that was made to the application or configuration. The following command can be used to roll back to a previous revision of a Deployment object:

```bash
kubectl rollout undo deployment nginx-deployment
```

```bash
kubectl rollout undo deployment nginx-deployment --to-revision=2
```