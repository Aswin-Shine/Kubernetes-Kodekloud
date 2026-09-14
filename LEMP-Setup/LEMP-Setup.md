Solution :

1. Check the namespaces and pods running.

```
kubectl get namespaces; kubectl get pods
```

2. Create all the secretes mentioned in the question.

```
kubectl create secret generic mysql-root-pass \
--from-literal=password=R00t \

kubectl create secret generic mysql-user-pass \
  --from-literal=username=kodekloud_gem \
  --from-literal=password=TmPcZjtRQx

kubectl create secret generic mysql-db-url \
  --from-literal=database=kodekloud_db4

kubectl create secret generic mysql-host \
  --from-literal=host=127.0.0.1
```

3. Create deployment yaml file.

```
vi lemp-dev.yaml

apiVersion: v1
kind: ConfigMap
metadata:
   name: php-config
data:
   php.ini: |
     variables_order = "EGPCS"

---
apiVersion: apps/v1
kind: Deployment
metadata:
  name: lemp-wp
  labels:
    app: lemp
spec:
  replicas: 1
  selector:
    matchLabels:
      app: lemp
  template:
    metadata:
      labels:
        app: lemp
    spec:
      volumes:
        - name: php-config
          configMap:
            name: php-config
      containers:
        - name: nginx-php-container
          image: webdevops/php-nginx:alpine-3-php7
          ports:
          - containerPort: 80
          volumeMounts:
          - name: php-config
            mountPath: /opt/docker/etc/php/php.ini
            subPath: php.ini
          env:
          - name: MYSQL_ROOT_PASSWORD
            valueFrom:
              secretKeyRef:
                name: mysql-root-pass
                key: password
          - name: MYSQL_DATABASE
            valueFrom:
              secretKeyRef:
                name: mysql-db-url
                key: database
          - name: MYSQL_USER
            valueFrom:
              secretKeyRef:
                name: mysql-user-pass
                key: username
          - name: MYSQL_PASSWORD
            valueFrom:
              secretKeyRef:
                name: mysql-user-pass
                key: password
          - name: MYSQL_HOST
            valueFrom:
              secretKeyRef:
                name: mysql-host
                key: host
        - name: mysql-container
          image: mysql:5.6
          ports:
          - containerPort: 3306
          env:
          - name: MYSQL_ROOT_PASSWORD
            valueFrom:
              secretKeyRef:
                name: mysql-root-pass
                key: password
          - name: MYSQL_DATABASE
            valueFrom:
              secretKeyRef:
                name: mysql-db-url
                key: database
          - name: MYSQL_USER
            valueFrom:
              secretKeyRef:
                name: mysql-user-pass
                key: username
          - name: MYSQL_PASSWORD
            valueFrom:
              secretKeyRef:
                name: mysql-user-pass
                key: password
          - name: MYSQL_HOST
            valueFrom:
              secretKeyRef:
                name: mysql-host
                key: host
---
apiVersion: v1
kind: Service
metadata:
  name: lemp-service
spec:
  type: NodePort
  selector:
    app: lemp
  ports:
    - port: 80
      targetPort: 80
      nodePort: 30008
---
apiVersion: v1
kind: Service
metadata:
  name: mysql-service
spec:
  selector:
    app: lemp
  ports:
  - name: mysql
    protocol: TCP
    port: 3306
    targetPort: 3306
```

4. Apply the yaml file and check pods are runnig or not.

```

kubectl apply -f lemp-dev.yaml
kubectl get pods
```

5. Change index.php

```
vi tmp/index.php

<?php
$dbname = $_ENV["MYSQL_DATABASE"];
$dbuser = $_ENV["MYSQL_USER"];
$dbpass = $_ENV["MYSQL_PASSWORD"];
$dbhost = $_ENV["MYSQL_HOST"];

$connect = mysqli_connect($dbhost, $dbuser, $dbpass) or die("Unable to Connect to '$dbhost'");

$test_query = "SHOW TABLES FROM $dbname";
$result = mysqli_query($test_query);

if ($result->connect_error) {
   die("Connection failed: " . $conn->connect_error);
}
  echo "Connected successfully";

```

6. Copy new index.php to container

```
kubectl cp /tmp/index.php lemp-wp-6fc87855f-srzkt:/app -c
nginx-php-container
```