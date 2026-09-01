One of the DevOps team member was trying to install a WordPress website on a LAMP stack which is essentially deployed on Kubernetes cluster. It was working well and we could see the installation page a few hours ago. However something is messed up with the stack now due to a website went down. Please look into the issue and fix it:


FYI, deployment name is lamp-wp and its using a service named lamp-service. The Apache is using http default port and nodeport is 30008. From the application logs it has been identified that application is facing some issues while connecting to the database in addition to other issues. Additionally, there are some environment variables associated with the pods like MYSQL_ROOT_PASSWORD, MYSQL_DATABASE,  MYSQL_USER, MYSQL_PASSWORD, MYSQL_HOST.

Solution :

1. Check for the namespaces and pods running. 
```
kubectl get namespaces
kubectl get pods 
```

2. Check for the svc 
```
kubectl get svc 
```

3. Edit the svc 
```
kubectl edit svc lamp-service
*Change port from 8080 to 80*
```

4. Now check the logs of the pod 
```
kubectl logs lamp-wp-56c7c454fc-7fk2d 

*PHP Parse Error (500 Internal Server Error), I have encountered this error which is found on line 4 of /app/index.php *
```

5. Get into the pods/container and change the /app/index.php file 
```
kubectl exec -it lamp-wp-56c7c454fc-7fk2d -- /bin/bash
vi /app/index.php

*[''MYSQL_PASSWORD"" -------> 'MYSQL_PASSWORD']*
*['MYSQL-HOST' -------> 'MYSQL_HOST']*
```

6. Check pods are running or not 
```
kubectl get pods 
```