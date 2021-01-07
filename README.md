# Testing Kubernetes cluster creation and monitoring on public cloud (AWS)
These are the steps/tools for accomplishing this :
 # 1- Create EC2 instance on AWS and install:Ansible, kubectl, aws cli then create the k8 cluster via eksctl and automate that via Ansible playbook
 # 2- Deploy the app (in this case nginx) via kubectl on the newly created EC2 instance and automate that via Ansible playbook.
 # 3- Deploy Prometheus on k8 (Deployment, Service, Config-map, Persistent volume, Alertmanager) and add the targets to be monitored, for nginx there is a designated export used for that : for reference : https://github.com/martin-helmich/prometheus-nginxlog-exporter.
 # 4- configure prometheus alerts , for this case study an alert will be triggered if 10% of the memory usage of a pod in k8 cluster.
 # 5- add notifier to send an email once an alert is fired via smtp to send an email to my gmail email.
 # 6- configured slack webhook to send that alert via HTTP to specific slack channel.
  


#Step-1: Creation of Kubernetes Cluster via Ansible playbook :
 Folder: [k8-cluster]  k8s-cluster-creation.yml: This file uses eksctl command via aws cli to create the k8s cluster via aws EKS.
#Step-2: Deploying an Application (nginx) on the K8 created in step1:
 Folder: [Application] k8s-app-deployment.yml : This file uses application configuration file and parse them to kubectl to deploy nginx, a namespace has to be created before k8s-app-deployment.yml , for the creation of the namespace k8s-namespace-creation.yml is used


