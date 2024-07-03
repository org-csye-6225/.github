# NodeJS RESTful API and Cloud Infrastructure Project

## Overview

This project demonstrates the deployment and management of a Health Check RESTful API integrated within a comprehensive cloud infrastructure. Utilizing AWS and GCP services, the project highlights automated CI/CD pipelines, infrastructure provisioning with Terraform, and robust health monitoring to maintain optimal application performance.

## Table of Contents

- [Overview](#overview)
- [Features](#features)
- [Architecture](#architecture)
- [Getting Started](#getting-started)
- [Health Check API](#health-check-api)
- [Infrastructure Setup](#infrastructure-setup)
- [Deployment](#deployment)
- [Security and Compliance](#security-and-compliance)
- [Monitoring and Logging](#monitoring-and-logging)
- [CI/CD Pipeline](#cicd-pipeline)

## Features

- **Health Check API**: Endpoint to monitor application and database health.
- **Automated CI/CD Pipelines**: Continuous integration and deployment using GitHub Actions.
- **Infrastructure as Code**: Terraform scripts to provision and manage cloud resources.
- **Scalability and Security**: Autoscaling, load balancing, and encryption using GCP/AWS services.
- **Domain and DNS Management**: Secure HTTPS access via Cloud DNS and SSL certificates.
- **Robust Monitoring**: Structured logging and application health monitoring.

## Architecture

The project architecture consists of several key components deployed on AWS/GCP:

1. **Health Check API**: A Node.js-based REST API with a `/healthz` endpoint.
2. **Cloud Infrastructure**: Managed through Terraform, includes VPCs, subnets, and CloudSQL instances.
3. **CI/CD Pipelines**: Automated using GitHub Actions to build, test, and deploy code.
4. **Load Balancer and Autoscaler**: Ensures high availability and performance based on health checks.
5. **Custom VM Images**: Built with Packer and deployed to GCP/AWS instances.


## Getting Started

### Prerequisites

- AWS or GCP account with appropriate permissions.
- [Terraform](https://www.terraform.io/downloads.html) installed.
- [GitHub CLI](https://cli.github.com/) installed.
- [Docker](https://www.docker.com/products/docker-desktop) installed.
- [Packer](https://www.packer.io/downloads) installed.
- [gcloud CLI](https://cloud.google.com/sdk/docs/install) installed for GCP.

### Setup

1. **Clone the repository**:
   ```bash
   git clone https://github.com/your-username/your-repository.git
   cd your-repository
   ```
2. **Configure environment variables**:
Create a .env file with your specific environment variables:
```bash
  DB_HOST=<your-database-host>
  DB_USER=<your-database-user>
  DB_PASSWORD=<your-database-password>
```
3. **Install Dependencies**:
Create a .env file with your specific environment variables:
```bash
  npm install
```
4. **Initialize Terraform:**:
Create a .env file with your specific environment variables:
```bash
  terraform init
```

## Health Check API

The Health Check API provides an endpoint to monitor the health of the application and its connection to the database.

### Endpoint

- **GET /healthz**: Returns `200 OK` if the application can connect to the database; otherwise, returns `503 Service Unavailable`.

### API Details

- **No Caching**: Responses include `Cache-Control: no-cache`.
- **No Payloads**: Returns `400 Bad Request` if a payload is present in the request.

## Infrastructure Setup

The project utilizes Terraform to define and manage the cloud infrastructure.

### Steps to Deploy Infrastructure

1. **Edit Terraform Variables**:
   Modify `terraform.tfvars` to configure your infrastructure parameters:
   ```hcl
   region         = "us-central1"
   vpc_cidr       = "192.168.0.0/16"
   subnet1_cidr   = "192.168.1.0/24"
   subnet2_cidr   = "192.168.2.0/24"

2. **Apply Terraform Configuration**:
  ```bash
   terraform apply -var-file="terraform.tfvars"
  ```

# Deployment

## Deploying the Application

1. **Build the Application**:

    ```bash
    npm run build # or your specific build command
    ```

2. **Deploy with Docker**:

    ```bash
    docker build -t your-image-name .
    docker run -d -p 80:80 --name your-container-name your-image-name
    ```

## Using Packer

1. **Build Custom Image**:

    ```bash
    packer build packer-template.json
    ```

2. **Deploy Custom Image**: Use the GCP/AWS console or CLI to deploy the custom image to your VM instances.

## Security and Compliance

* **IAM Roles and Policies**: Managed via Terraform to restrict access.
* **Encryption**: Configured using CMEK for VMs and databases.
* **Branch Protection**: Implemented in GitHub to enforce secure code practices.

## Monitoring and Logging

* **Structured Logs**: Application logs are in JSON format and streamed to Google Cloud Logging.
* **Health Monitoring**: The `/healthz` endpoint is used for load balancer health checks and autoscaling.

## CI/CD Pipeline

GitHub Actions are used to automate the CI/CD process:

* **Build and Test**: Automated on pull request events.
* **Deploy**: Triggered upon merging to the main branch, using Terraform for infrastructure and Docker for application deployment.

