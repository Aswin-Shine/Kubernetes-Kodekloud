There is a production deployment planned for next week. The Nautilus DevOps team wants to test the deployment update and rollback on Dev environment first so that they can identify the risks in advance. Below you can find more details about the plan they want to execute.

Create a namespace nautilus. Create a deployment called httpd-deploy under this new namespace, It should have one container called httpd, use httpd:2.4.25 image and 4 replicas. The deployment should use RollingUpdate strategy with maxSurge=1, and maxUnavailable=2. Also create a NodePort type service named httpd-service and expose the deployment on nodePort: 30008.

Now upgrade the deployment to version httpd:2.4.43 using a rolling update.

Finally, once all pods are updated undo the recent update and roll back to the previous/original version.

Solution :

1. Check all the namespaces and pods.

```
kubectl get namespaces
kubect get pods
```

2. Create yaml file

```
vi httpd-dev.yaml

apiVersion: v1
kind: Namespace
metadata:
  name: nautilus
---
apiVersion: apps/v1
kind: Deployment
metadata:
  name: httpd-deploy
  namespace: nautilus
spec:
  replicas: 4
  strategy:
    type: RollingUpdate
    rollingUpdate:
      maxSurge: 1
      maxUnavailable: 2
  selector:
    matchLabels:
      app: httpd-app
  template:
    metadata:
      labels:
        app: httpd-app
    spec:
      containers:
      - name: httpd
        image: httpd:2.4.25
---
apiVersion: v1
kind: Service
metadata:
  name: httpd-service
  namespace: nautilus
spec:
  type: NodePort
  selector:
    app: httpd-app
  ports:
    - port: 80
      targetPort: 80
      nodePort: 30008
```

3. Apply the yaml file

```
kubectl apply -f httpd-dev.yaml
```

4. Check pods are running or not.

```
kubectl get pods -n nautilus
```

5. Rolling Update command

```
kubectl set image deployment/httpd-deploy httpd=httpd:2.4.43 -n nautilus
```

6. Rolling Update Status command

```
kubectl rollout status deployment/httpd-deploy -n nautilus
```

7. Rollback command

```
kubectl rollout undo deployment/httpd-deploy -n nautilus
```

8. Check pods are running or not.

```
kubectl get pods -n nautilus
```
