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
