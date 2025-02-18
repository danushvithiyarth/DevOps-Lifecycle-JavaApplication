# DevOps Lifecycle for Java Application with Kubernetes Ingress

## Project Overview

This project demonstrates a complete DevOps lifecycle for a Java application, integrating CI/CD, containerization, security scanning, and Kubernetes deployment with Ingress routing. The application is hosted under a custom domain (danushvithiyarth.in), including path-based routing for /dev.

## Key Highlights

Automated Infrastructure Provisioning: Used Terraform to create AWS EC2 instances and security groups.

Docker Image Creation: Built a multi-stage Dockerfile for efficient Java application containerization.

Continuous Integration (CI): Jenkins pipeline with Maven build, SonarQube analysis, and Trivy security scans.

Containerization: Built and pushed Docker images to Docker Hub.

Kubernetes Deployment: Managed EKS cluster and deployed Java application using Kubernetes manifests.

Ingress Path-Based Routing: Configured NGINX Ingress to serve the application under danushvithiyarth.in and /dev.

# Step-by-Step Process

## Infrastructure Setup with Terraform

Provisioned AWS EC2 instances for Jenkins and Kubernetes deployment.

Configured security groups and access rules without manual AWS Dashboard modifications.

## Docker Image Creation with Multi-Stage Build

Created a multi-stage Dockerfile:

Used maven:latest for building the application.

Used openjdk:25-oraclelinux9 for running the final application.

Optimized the image size and ensured efficient dependency management.

Built and pushed the Docker image to Docker Hub.

## CI/CD Pipeline with Jenkins

Installed Jenkins with required plugins (SonarQube scanner, Stage View, Maven, etc.).

Configured SonarQube server for static code analysis.

Integrated Trivy to generate vulnerability reports for Docker images.

Successfully triggered automated builds via Git Webhooks.

## Kubernetes Deployment with AWS EKS

Installed AWS CLI, eksctl, and configured Kubeconfig.

Created an EKS Cluster and a dedicated namespace (java-deployment).

Deployed the application with replica management (HPA), ClusterIP service, and ingress routing.

## Ingress Path-Based Routing

Configured NGINX Ingress Controller using Helm.

Deployed Ingress rules to expose services under danushvithiyarth.in and danushvithiyarth.in/dev.

Verified successful routing for both the Java application and an Nginx-based service under /dev.

# Outcome

 Successfully built an automated DevOps lifecycle for a Java application.
 Achieved seamless CI/CD with Jenkins, SonarQube, and Docker image security scanning.
 Deployed a scalable application on AWS EKS with domain-based Ingress routing.

