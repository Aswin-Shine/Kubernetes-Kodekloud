A junior DevOps team member encountered difficulties deploying a stack on the Kubernetes cluster. The pod fails to start, presenting errors. Let's troubleshoot and rectify the issue promptly.

There is a pod named webserver, and the container within it is named httpd-container, its utilizing the httpd:latest image.

Additionally, there's a sidecar container named sidecar-container using the ubuntu:latest image.

Solution :

1. Check the namespaces and pods running.

```

kubectl get namespaces
kubectl get pods
```

2. Descirbe the affected pods

```
kubectl describe pod webserver
```

3. Edit pod the affected pod (In my case there was a typo in image name)

```
kubectl edit pod webserver
```

4. Check the pod is running.

```
kubectl get pods
```
