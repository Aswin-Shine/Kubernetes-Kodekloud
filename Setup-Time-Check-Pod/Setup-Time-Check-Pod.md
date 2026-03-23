The Nautilus DevOps team needs a time check pod created in a specific Kubernetes namespace for logging purposes. Initially, it's for testing, but it may be integrated into an existing cluster later. Here's what's required:

Create a pod called time-check in the devops namespace. The pod should contain a container named time-check, utilizing the busybox image with the latest tag (specify as busybox:latest).

Create a config map named time-config with the data TIME_FREQ=10 in the same namespace.

Configure the time-check container to execute the command: while true; do date; sleep $TIME_FREQ;done. Ensure the result is written /opt/data/time/time-check.log. Also, add an environmental variable TIME_FREQ in the container, fetching its value from the config map TIME_FREQ key.

Create a volume log-volume and mount it at /opt/data/time within the container.

Solution :

1. Check all the namesapces and pods

```
kubectl get namespaces
kubectl get pods

```

2. Create pod.yaml file

```
vi pod.yaml

apiVersion: v1
kind: Namespace
metadata:
  name: devops
---
apiVersion: v1
kind: ConfigMap
metadata:
  name: time-config
  namespace: devops
data:
  TIME_FREQ: "10"
---
apiVersion: v1
kind: Pod
metadata:
  name: time-check
  namespace: devops
  labels:
    app: time-check
spec:
  volumes:
    - name: log-volume
      emptyDir: {}
  containers:
    - name: time-check
      image: busybox:latest
      volumeMounts:
        - mountPath: /opt/data/time
          name: log-volume
      envFrom:
        - configMapRef:
            name: time-config
      command: ["/bin/sh", "-c", "while true; do date; sleep $TIME_FREQ;done > /opt/security/time/time-check.log",
        ]
```

3. Apply the yaml file

```
kubectl apply -f pod.yaml
```

4. Check pods are running or not in the namespace

```
kubectl get pods -n devops
```
