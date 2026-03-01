The Nautilus DevOps team is setting up recurring tasks on different schedules. Currently, they're developing scripts to be executed periodically. To kickstart the process, they're creating cron jobs in the Kubernetes cluster with placeholder commands. Follow the instructions below:

Create a cronjob named nautilus.

Set Its schedule to something like _/5 _ \* \* \*. You can set any schedule for now.

Name the container cron-nautilus.

Utilize the httpd image with latest tag (specify as httpd:latest).

Execute the dummy command echo Welcome to xfusioncorp!.

Ensure the restart policy is OnFailure.

Solution :

1. Make a directory or change to any directory

```
cd /tmp
```

2. Create cronjob.yaml file

```
vi cronjob.yaml

apiVersion: batch/v1
kind: CronJob
metadata:
  name: nautilus
spec:
  schedule: "*/2 * * * *"
  jobTemplate:
    spec:
      template:
        spec:
          containers:
            - name: cron-nautilus
              image: nginx:latest
              command:
                - /bin/sh
                - -c
                - echo Welcome to xfusioncorp
          restartPolicy: OnFailure
```

3. Apply this file

```
kubectl apply -f cronjob.yaml
```

4. Verify the pods and cronjob

```
kubectl get pods
kubectl get cronjobs
```

5. Describe cronjob

```

kubectl describe cronjob nautilus
```
