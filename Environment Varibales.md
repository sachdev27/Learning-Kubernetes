# Environment Variables 


## Environment Variables in Config file

Environment variables can be used in the config file using the syntax `${ENV_VAR}`. The following example shows how to use environment variables in the config file:

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
            value: ${APP_COLOR}
```


## ValueFrom Field

The valueFrom field can be used to set the value of an environment variable using a field reference. The following example shows how to use the valueFrom field to set the value of an environment variable using a field reference:

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
              fieldRef:
                fieldPath: metadata.name
```