The Nautilus DevOps team is crafting jobs in the Kubernetes cluster. While they're developing actual scripts/commands, they're currently setting up templates and testing jobs with dummy commands. Please create a job template as per details given below:

Create a job named countdown-devops.

The spec template should be named countdown-devops (under metadata), and the container should be named container-countdown-devops

Utilize image ubuntu with latest tag (ensure to specify as ubuntu:latest), and set the restart policy to Never.

Execute the command sleep 5

Solution :

1. Check pods are running.

```

kubectl get pods
```

2. Make a directory or change your current directory

```
cd /tmp
```

3. Create countdown-job.yaml file

```
vi countdown-job.yaml

apiVersion: batch/v1
kind: Job
metadata:
  name: countdown-devops
spec:
  template:
    metadata:
      name: countdown-devops
    spec:
      containers:
        - name: container-countdown-devops
          image: debian:latest
          command: ["/bin/sh", "-c", "sleep 5" ]
      restartPolicy: Never

```

4. Apply the yaml file

```

kubectl apply -f countdown-job.yaml
```

5. Check the pods is running or not

```
kubectl get pods
```
