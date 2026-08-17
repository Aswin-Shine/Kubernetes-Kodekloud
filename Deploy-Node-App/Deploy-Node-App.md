The Nautilus development team has completed development of one of the node applications, which they are planning to deploy on a Kubernetes cluster. They recently had a meeting with the DevOps team to share their requirements. Based on that, the DevOps team has listed out the exact requirements to deploy the app. Find below more details:

Create a deployment using gcr.io/kodekloud/centos-ssh-enabled:node image, replica count must be 2.

Create a service to expose this app, the service type must be NodePort, targetPort must be 8080 and nodePort should be 30012.

Make sure all the pods are in Running state after the deployment.

Solution :

1. Get all the namespaces and pods running.

```
kubectl get namesapces
kubectl get pods
```

2. Create the yaml file

```
vi node-dev.yaml

apiVersion: apps/v1
kind: Deployment
metadata:
  name: node-deployment
  labels:
    app: node-enabled
spec:
  replicas: 2
  selector:
    matchLabels:
      app: node-enabled
  template:
    metadata:
      labels:
        app: node-enabled
    spec:
      containers:
      - name: node-container
        image: gcr.io/kodekloud/centos-ssh-enabled:node
        ports:
        - containerPort: 8080
---
apiVersion: v1
kind: Service
metadata:
  name: node-service
spec:
  type: NodePort
  selector:
    app: node-enabled
  ports:
    - port: 8080
      targetPort: 8080
      nodePort: 30012

```

3. Apply yaml file

```
kubectl get pods -n iron-namespace-devops
```
4. Check pods are running or not. 
```
kubectl get pods 
```