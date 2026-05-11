# Project 3 — Automated CI/CD Deployment Pipeline

Production-style CI/CD deployment pipeline built using Docker, GitHub Actions, AWS EC2, and Nginx reverse proxying.

---

## Overview

This project demonstrates an automated deployment workflow where code pushed to GitHub is automatically deployed to an AWS EC2 server using GitHub Actions.

The application runs inside a Docker container and is exposed publicly through an Nginx reverse proxy configuration.

The project focuses heavily on:

- CI/CD automation
- Docker container deployments
- Reverse proxy architecture
- Deployment validation
- Linux server administration
- Cloud security and operational workflows

---

## Architecture

```text
Developer Pushes Code
        ↓
GitHub Actions Workflow
        ↓
SSH Deployment to AWS EC2
        ↓
deploy.sh Execution
        ↓
Docker Container Rebuild
        ↓
Nginx Reverse Proxy
        ↓
Live Production Application
```

---

## Technologies Used

- AWS EC2
- Docker
- Docker Compose
- Nginx
- GitHub Actions
- Ubuntu Linux
- Git & GitHub

---

# Features

- Automated CI/CD deployment pipeline
- Dockerized web application
- GitHub Actions workflow automation
- Nginx reverse proxy configuration
- Deployment validation workflow
- Secure AWS Security Group configuration
- Linux deployment scripting
- Container lifecycle management

---

# Project Structure

```text
project3-cicd-deployment-pipeline/
│
├── .github/workflows/
│   └── deploy.yml
│
├── Dockerfile
├── docker-compose.yml
├── deploy.sh
├── index.html
└── README.md
```

---

# Deployment Workflow

## 1. Developer Pushes Code

Code changes are pushed to the GitHub repository.

## 2. GitHub Actions Triggered

GitHub Actions automatically starts the deployment workflow.

## 3. Secure SSH Connection to EC2

The workflow connects securely to the EC2 server using SSH secrets stored in GitHub.

## 4. Automated Deployment Script Executes

The deployment script performs:

- Git pull
- Docker rebuild
- Container restart
- Deployment validation
- Nginx reload

## 5. Application Deployment Completed

The updated application becomes publicly accessible through Nginx.

---

# Docker Deployment

## Build and Start Containers

```bash
docker compose up -d --build
```

## Stop Containers

```bash
docker compose down
```

## Verify Running Containers

```bash
docker compose ps -a
```

---

# Nginx Reverse Proxy

Nginx was configured as a reverse proxy to forward public HTTP traffic from port 80 to the Docker container running internally on port 8080.

Example configuration:

```nginx
server {
    listen 80;
    server_name _;

    location / {
        proxy_pass http://127.0.0.1:8080;
        proxy_http_version 1.1;

        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
        proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
        proxy_set_header X-Forwarded-Proto $scheme;
    }
}
```

---

# CI/CD Pipeline

GitHub Actions automatically deploys updates to the EC2 server when code is pushed to the `main` branch.

Workflow highlights:

- Automated deployment
- SSH-based remote execution
- Docker container rebuild
- Deployment validation
- Nginx reload

Example deployment trigger:

```yaml
on:
  push:
    branches:
      - main
```

---

# Security Configuration

AWS Security Groups were configured to:

| Port | Purpose |
|---|---|
| 80 | Public HTTP access |
| 22 | Restricted SSH administrative access |

Public access to container port `8080` was removed after validating the reverse proxy deployment.

---

# Deployment Validation

Deployment validation included:

- Container health verification
- Browser accessibility testing
- Nginx status validation
- Reverse proxy testing
- GitHub Actions workflow validation

---

# Screenshots

## GitHub Actions Successful Deployment

Rename image to:

```text
github-actions-successful-deployment.png
```

Markdown:

```md
![GitHub Actions Deployment](images/github-actions-successful-deployment)
```

---

## Nginx Reverse Proxy Configuration

Rename image to:

```text
nginx-reverse-proxy-configuration.png
```

Markdown:

```md
![Nginx Reverse Proxy](images/nginx-reverse-proxy-configuration)
```

---

## Nginx Service Running

Rename image to:

```text
nginx-service-running.png
```

Markdown:

```md
![Nginx Service](images/nginx-service-running)
```

---

## AWS Security Group Configuration

Rename image to:

```text
aws-security-group-configuration.png
```

Markdown:

```md
![AWS Security Group](images/aws-security-group-configuration)
```

---

## Docker Compose Container Status

Rename image to:

```text
docker-compose-container-status.png
```

Markdown:

```md
![Docker Compose Status](images/docker-compose-container-status)
```

---

# Lessons Learned

This project strengthened hands-on experience with:

- CI/CD pipeline automation
- Docker deployments
- Linux operations
- Reverse proxy architecture
- AWS networking and security
- SSH deployment workflows
- Deployment troubleshooting
- Infrastructure operational practices

---

# Future Improvements

- HTTPS with Let's Encrypt
- Rollback deployment strategy
- Health endpoint monitoring
- Self-hosted GitHub Actions runner
- Docker image registry integration
- Deployment notifications
- Centralized logging and monitoring

---

# Author

Demarko Little

- GitHub: https://github.com/dlittle-source
- LinkedIn: https://linkedin.com/in/demarkol