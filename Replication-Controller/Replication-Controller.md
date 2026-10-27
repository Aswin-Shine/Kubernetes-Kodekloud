The Nautilus DevOps team is establishing a ReplicationController to deploy multiple pods for hosting applications that require a highly available infrastructure. Follow the specifications below to create the ReplicationController:

Create a ReplicationController using the httpd image with latest tag, and name it httpd-replicationcontroller.

Assign labels app as httpd_app, and type as front-end. Ensure the container is named httpd-container and set the replica count to 3.


All pods should be running state post-deployment.

Solution :

1. Check the namespaces and pods running

```
kubectl get namespaces
kubect get pods
```

2. Create pod.yaml file

```
vi pod. yaml

apiVersion: v1
kind: ReplicationController
metadata:
  name: httpd-replicationcontroller
  labels:
    app: httpd_app
    type: front-end
spec:
  replicas: 3
  selector:
    app: httpd_app
  template:
    metadata:
      name: httpd_pod
      labels:
        app: httpd_app
        type: front-end
    spec:
      containers:
        - name: httpd-container
          image: httpd:latest
          ports:
            - containerPort: 80
```

4. Apply the yaml file

```
kubectl apply -f pod.yaml
```

5. Check pods are running or not

```
kubectl get pods
```
