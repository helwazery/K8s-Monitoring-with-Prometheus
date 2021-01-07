# Testing Kubernetes cluster creation and monitoring on public cloud (AWS)
These are the steps/tools for accomplishing this :
### 1- Create EC2 instance on AWS and install:Ansible, kubectl, aws cli then create the k8 cluster via eksctl and automate that via Ansible playbook
####Folder: [k8-cluster]  k8s-cluster-creation.yml: This file uses eksctl command via aws cli to create the k8s cluster via aws EKS. 

### 2- Deploy the app (in this case nginx) via kubectl on the newly created EC2 instance and automate that via Ansible playbook.
####Folder: [Application] k8s-app-deployment.yml : This file uses application configuration file and parse them to kubectl to deploy nginx, a namespace has to be created before k8s-app-deployment.yml , for the creation of the namespace k8s-namespace-creation.yml is used

### 3- Deploy Prometheus on k8 (Deployment, Service, Config-map, Persistent volume, Alertmanager) and add the targets to be monitored, for nginx there is a designated export used for that : for reference : https://github.com/martin-helmich/prometheus-nginxlog-exporter.
#### Folder: [Prometheus] and Folder [application-nginx-monitoring]  prometheus-deployment-automation.yml : This file automates the deployment of Prometheus (including Service, Config-map, Deployment) via namespace called monitoring which will be created as a pre-requiste before deploying Prometheus-deployment-automation.yml via this file: monitoring-namespace-creation.yml

### 4- configure prometheus alerts , for this case study an alert will be triggered if 10% of the memory usage of a pod in k8 cluster.
#### Folder: [Alertmanager] Deploy-Alertmanager.yml is for automation of deploying the alertmanager and deploying the alerts , in this case the alert is for monitoring the memory usage of pod .
### 5- add notifier to send an email once an alert is fired via smtp to send an email to my gmail email.
#### Folder: [Alertmanager-config-map.yml] contains the receiver and in this case it is the smtp to send an alert for my gmail email. 
### 6- configured slack webhook to send that alert via HTTP to specific slack channel.
#### Folder: [Alertmanager-config-map.yml] contains the receivers and the API url of the slack webhook for the alerts
  




