# Kubernetes : KodeKloud

My hands-on solutions to the Kubernetes tasks from **[KodeKloud Engineer](https://engineer.kodekloud.com/)**. Each folder is one task: the problem statement, the `kubectl` commands and YAML manifests I used to solve it, and screenshots of the result.

Every task runs on KodeKloud's lab Kubernetes cluster, reached from the jump host, for the fictional Nautilus / xFusionCorp teams.

![Tasks](https://img.shields.io/badge/tasks-28-blue) ![Kubernetes](https://img.shields.io/badge/-Kubernetes-326CE5?logo=kubernetes&logoColor=white) ![kubectl](https://img.shields.io/badge/-kubectl-326CE5?logo=kubernetes&logoColor=white) ![YAML](https://img.shields.io/badge/-YAML-CB171E?logo=yaml&logoColor=white)

## 📂 Repository structure

```text
.
└── <Task-Name>/
    ├── <Task-Name>.md      # Problem statement + step-by-step solution
    └── Screenshot/         # Proof of completion
```

## 📊 Progress at a glance

| Topic | Tasks |
|---|---|
| 🧱 Pods, Jobs and configuration | 8 |
| 🚀 Deployments and Services | 9 |
| 💾 Storage and stateful apps | 3 |
| 🧩 Multi-tier stacks | 4 |
| 🔧 Troubleshooting | 4 |
| **Total** | **28** |

> Task numbers follow the commit history (`Task 1` to `Task 28`).

## 🗂️ Tasks

### 🧱 Pods, Jobs and configuration

Pods, Jobs and CronJobs, plus ConfigMaps, Secrets, environment variables and init containers.

| # | Task | Solution |
|:---:|---|---|
| 1 | CronJob running a placeholder command every 5 minutes | [Schedule-CronJob](Schedule-CronJob/Schedule-CronJob.md) |
| 2 | One-off Job with `restartPolicy: Never` | [Countdown-Job](Countdown-Job/Countdown-Job.md) |
| 3 | Logging pod driven by a ConfigMap, writing to a mounted volume | [Setup-Time-Check-Pod](Setup-Time-Check-Pod/Setup-Time-Check-Pod.md) |
| 19 | Expose pod and node fields as env vars with `fieldRef` | [Environment-Variables](Environment-Variables/Environment-Variables.md) |
| 22 | Init container that prepares a shared volume | [Init-Containers](Init-Containers/K8S-Init-Containers.md) |
| 24 | Create a Secret from a file and mount it in a pod | [Manage-Secrets](Manage-Secrets/K8S-Manage-Secrets.md) |
| 27 | Create a labelled pod | [Pod-Creation](Pod-Creation/K8S-Pod-Creation.md) |
| 28 | Pass and print environment variables | [Print-Env-Variables](Print-Env-Variables/K8S-Print-Env-Variables.md) |

### 🚀 Deployments and Services

Deploying apps with replicas, namespaces and NodePort Services.

| # | Task | Solution |
|:---:|---|---|
| 5 | Apache in its own namespace, 2 replicas, NodePort Service | [Deploy-Apache-App](Deploy-Apache-App/Deploy-Apache-App.md) |
| 6 | Create an httpd Deployment | [App-Deployment](App-Deployment/K8S-App-Deployment.md) |
| 7 | Deploy Grafana behind a NodePort Service | [Deploy-Grafana](Deploy-Grafana/K8S-Deploy-Grafana.md) |
| 10 | Iron Gallery app with a MariaDB database and Services | [Deploy-Iron-Gallery](Deploy-Iron-Gallery/K8S-Deploy-Iron-Gallery.md) |
| 11 | Jenkins server in its own namespace | [Deploy-Jenkins](Deploy-Jenkins/Deploy-Jenkins.md) |
| 15 | Node.js app with 2 replicas | [Deploy-Node-App](Deploy-Node-App/Deploy-Node-App.md) |
| 16 | Redis configured through a ConfigMap, with CPU requests | [Deploy-Redis](Deploy-Redis/K8S-Deploy-Redis.md) |
| 17 | Tomcat app in its own namespace | [Deploy-Tomcat](Deploy-Tomcat/Deploy-Tomcat.md) |
| 25 | Highly available Nginx Deployment (3 replicas) | [Nginx-Deployment](Nginx-Deployment/K8S-Nginx-Deployment.md) |

### 💾 Storage and stateful apps

PersistentVolumes, PersistentVolumeClaims and databases that keep their data.

| # | Task | Solution |
|:---:|---|---|
| 8 | Drupal with MySQL on a hostPath PersistentVolume | [Deploy-Drupal-App](Deploy-Drupal-App/Deploy-Drupal-App.md) |
| 13 | MySQL with PV, PVC and Secrets | [Deploy-MySql](Deploy-MySql/K8S-Deploy-MySQL.md) |
| 26 | Web server pod serving files from a PVC | [Persistent-Volume](Persistent-Volume/K8S-Persistent-Volume.md) |

### 🧩 Multi-tier stacks

Several containers or Deployments wired together with ConfigMaps, Secrets and Services.

| # | Task | Solution |
|:---:|---|---|
| 9 | Guestbook app: Redis master and replicas plus a PHP frontend | [Deploy-Guest-Book](Deploy-Guest-Book/K8S-Deploy-Guest-Book.md) |
| 12 | LAMP stack: Apache + PHP and MySQL in one pod, config from a ConfigMap and Secrets | [Deploy-LAMP-Stack](Deploy-LAMP-Stack/Deploy-LAMP-Stack.md) |
| 14 | Nginx + PHP-FPM sharing a volume, with a custom `nginx.conf` | [Deploy-Nginx-Phpfpm](Deploy-Nginx-Phpfpm/Deploy-Nginx-Phpfpm.md) |
| 23 | LEMP stack: Nginx + PHP and MySQL, credentials in Secrets | [LEMP-Setup](LEMP-Setup/LEMP-Setup.md) |

### 🔧 Troubleshooting

Finding and fixing broken pods and Deployments.

| # | Task | Solution |
|:---:|---|---|
| 4 | Fix a pod (httpd + sidecar) failing on a mistyped image name | [Resovle-Pod-Issue](Resovle-Pod-Issue/Resolve-Pod-Issue.md) |
| 18 | Fix a broken Redis Deployment | [Deployment-Troubleshoot](Deployment-Troubleshoot/K8S-Deployment-Troubleshoot.md) |
| 20 | Fix a WordPress LAMP stack that can't reach its database | [Fix-LAMP-Enivironment](Fix-LAMP-Enivironment/Fix-LAMP_Enivronment.md) |
| 21 | Fix a Flask app with the wrong image and targetPort | [Fix-Python-App](Fix-Python-App/K8S-Fix-Python-App.md) |

## 🚀 How to use this repo

1. Pick a topic above and open the task's `.md` file.
2. Read the problem statement at the top, then follow the **Solution** steps.
3. Check the `Screenshot/` folder to compare against the expected output.

> ⚠️ Names, passwords and NodePorts in these solutions belong to KodeKloud's temporary lab environment. Treat them as examples and change them before using anything in a real cluster.

## 🙏 Acknowledgements

Task scenarios are from [KodeKloud](https://kodekloud.com/) and the KodeKloud Engineer platform. The solutions and notes are mine.
