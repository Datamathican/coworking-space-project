# Coworking Space Service - EKS Deployment

## Project Overview
This project automates the deployment of a microservice-based Coworking Space application using AWS EKS and a CI/CD pipeline. The architecture consists of a Python Flask frontend and a PostgreSQL database backend.

## Cluster Configuration
The infrastructure is provisioned on AWS EKS using `eksctl` with a managed node group consisting of two `t3.medium` instances. Kubernetes resources include Deployments for scaling, Services for internal networking, and a LoadBalancer for external access. Storage for the database is managed through PersistentVolumeClaims using AWS EBS volumes.

## Build and Deployment Flow
The CI/CD pipeline is orchestrated via AWS CodeBuild, which triggers on every push to the repository. CodeBuild builds the Docker image from a Dockerfile, tags it with a version number, and pushes it to Amazon ECR. Upon a successful build, the updated image is manually or automatically deployed to the EKS cluster using `kubectl`.

## Releasing New Builds
To release a new version, developers push code changes to the GitHub repository. This initiates a new CodeBuild execution that updates the image in ECR. Finally, running `kubectl rollout restart deployment/coworking-app` ensures the cluster pulls the latest image without downtime.
