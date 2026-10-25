The Nautilus DevOps team is gearing up to deploy applications on a Kubernetes cluster for migration purposes. A team member has been tasked with creating a ReplicaSet outlined below:

Create a ReplicaSet using nginx image with latest tag (ensure to specify as nginx:latest) and name it nginx-replicaset.

Apply labels: app as nginx_app, type as front-end.

Name the container nginx-container. Ensure the replica count is 4.

Solution :

1. Make a directory or get into any directory

```

cd /tmp
```

2. Create nginx-deployment.yaml file

```
vi nginx-deployment.yaml

apiVersion: apps/v1
kind: ReplicaSet
metadata:
  name: nginx-replicaset
  labels:
    app: nginx_app
    type: front-end
spec:
  replicas: 4
  selector:
    matchLabels:
      app: nginx_app
  template:
    metadata:
      labels:
        app: nginx_app
        type: front-end
    spec:
      containers:
      - name: nginx-container
        image: nginx:latest
```

3. Apply this yaml file

```

kubectl apply -f nginx-deployment.yaml
```

4. Check pods are running or not.

```

kubectl get pods
```
