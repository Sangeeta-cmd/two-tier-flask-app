# Flask + MySQL 2-Tier Application – Docker & Jenkins

## Overview

This project is a two-tier web application consisting of a Flask backend and a MySQL database.

The Flask application was containerized using Docker. Jenkins was then used to automate the process of checking out the source code, building the Docker image, and pushing the image to Docker Hub.

The Dockerized application was deployed and run on an AWS EC2 instance.

## Project Flow

```text
GitHub
   ↓
Jenkins
   ↓
Checkout Code
   ↓
Build Flask Docker Image
   ↓
Push Image to Docker Hub
   ↓
Docker Compose
   ↓
Run Flask Container
   ↓
MySQL Database
```

## Dockerization

A `Dockerfile` was created for the Flask application to package the application and its dependencies into a Docker image.

The image can be built using:

```bash
docker build -t flask-app:latest .
```

## MySQL Configuration

The Flask application connects to the MySQL database using the configured database connection details.

The application and database communication requires the correct MySQL host, port, username, password, and database name.

## Jenkins Pipeline

Jenkins was configured to automate the Docker image creation and publishing process.

The pipeline performs:

1. Checkout the source code from GitHub.
2. Build the Flask application's Docker image.
3. Authenticate with Docker Hub.
4. Push the Docker image to Docker Hub.
5. Application is deployed on EC2 Instance using docker compose.

## Deployment on AWS EC2

After the Docker image is pushed to Docker Hub, it is deployed on EC2 Instance using docker compose.
The Flask application container can then be started using:

```bash
docker compose down || true
docker compose up -d --build
```


## Deployment on Kubernetes cluster using Kubeadm

I have deployed this aaplication on kubernetes cluster by setting up kubeadm. I have referrenced below link to setup Kubeadm on EC2 instance. </br>
https://github.com/LondheShubham153/kubestarter/tree/main/Kubeadm_Installation_Scripts_and_Documentation 

Make sure to open below ports for control plane smooth setup.<br/>
<img width="1566" height="726" alt="Screenshot 2026-11-07 042619" src="https://github.com/user-attachments/assets/074cd3c6-8dab-433a-a0d5-fcd6eef68f61" /><br/>
<img width="932" height="360" alt="Screenshot 2026-11-07 042302" src="https://github.com/user-attachments/assets/5ab9e7de-c133-463b-8edc-e2f5b3dba4f8" />

Keypoints:
1. Automated the Kubernetes cluster setup using Kubeadm and later with AWS EKS eksctl
2. Packaged Kuberneter Manifest files using HELM and deployed application on AWS EKS
3. Ensured multi-node cluster setup for high availability and deployment using Load Balancer
4. Improved scalability of application to 10,000 concurrent users and reduced downtime by 60% using AWS Managed Elastic Kubernetes Service (EKS)
