Jenkins CI server to create/manage some deployment pipelines for some of the projects. They want to set up the Jenkins server on Kubernetes cluster. Below you can find more details about the task:

1. Create a namespace jenkins

2. Create a Service for jenkins deployment. Service name should be jenkins-service under jenkins namespace, type should be NodePort, nodePort should be 30008

3. Create a Jenkins Deployment under jenkins namespace, It should be name as jenkins-deployment , labels app should be jenkins , container name should be jenkins-container , use jenkins/jenkins image , containerPort should be 8080 and replicas count should be 1.

Make sure to wait for the pods to be in running state and make sure you are able to access the Jenkins login screen in the browser before hitting the Check button.

Solution :

1. Check all the namespaces and pods running.

```
kubectl get namespaces
kubectl get pods
```

2. Create yaml file for jenkins

```
vi jenkins-dev.yaml

apiVersion: v1
kind: Namespace
metadata:
  name: jenkins
---
apiVersion: apps/v1
kind: Deployment
metadata:
  name: jenkins-deployment
  namespace: jenkins
  labels:
    app: jenkins
spec:
  replicas: 1
  selector:
    matchLabels:
      app: jenkins
  template:
    metadata:
      labels:
        app: jenkins
    spec:
      containers:
      - name: jenkins-container
        image: jenkins/jenkins
        ports:
        - containerPort: 8080
---
apiVersion: v1
kind: Service
metadata:
  name: jenkins-service
  namespace: jenkins
spec:
  type: NodePort
  selector:
    app: jenkins
  ports:
    - port: 8080
      targetPort: 8080
      nodePort: 30008

```

3. Apply the yaml file

```
kubectl apply -f jenkins-dev.yaml
```

4. Check the pods are running or not

```
kubectl get pods -n jenkins
```
