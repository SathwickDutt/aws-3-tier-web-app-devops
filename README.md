# AWS 3-Tier Web App on EKS with DevSecOps, CI/CD, and Observability

A production-style AWS DevOps project that demonstrates end-to-end deployment, security, automation, and monitoring for a 3-tier web application on Kubernetes.

## Overview

This project deploys a containerized web application on AWS EKS with:
- Frontend: React.js
- Backend: Node.js / Express
- Database: MySQL
- Containerization: Docker
- Orchestration: Kubernetes
- Cloud: AWS

The goal is to model a realistic enterprise DevOps workflow covering:
- secure CI/CD automation
- Kubernetes deployment
- AWS integration
- infrastructure security
- observability and monitoring

## Architecture Overview

The application is deployed in a containerized 3-tier architecture using AWS EKS, with an Application Load Balancer (ALB) routing traffic to the services, ACM for HTTPS certificates, and Route 53 for DNS management.

This setup also integrates:
- metrics collection
- dashboards
- centralized logging
- secret management
- secure AWS access

## Tech Stack

- AWS: EKS, EC2, ALB, Route 53, ACM, IAM, Secrets Manager, S3
- Containers & Orchestration: Docker, Kubernetes, StatefulSets, Persistent Volumes
- CI/CD: GitHub Actions
- DevSecOps: Gitleaks, Trivy, Checkov, SonarQube, linting, SBOM
- Authentication & Secrets: GitHub OIDC, IRSA, External Secrets Operator (ESO)
- Observability: Prometheus, Grafana, Loki, Alloy
- Application: React.js, Node.js, MySQL

## CI/CD Pipeline

The pipeline is designed around secure, production-ready delivery:

1. Source Control
   - Feature branch development
   - QA branch validation
   - Production branch promotion

2. Security & Quality Gates
   - Gitleaks for secret scanning
   - Trivy for filesystem and image vulnerability scans
   - Checkov for Terraform, Kubernetes, and Dockerfile scanning
   - SonarQube for code quality and quality gate enforcement
   - SBOM generation for source and image artifacts

3. Build & Publish
   - Build and scan Docker images
   - Publish verified images to a private registry

4. QA Deployment
   - Automated deployment to the QA environment
   - Manifest updates and rollout validation

5. Production Promotion
   - Separate production deployment flow
   - Branch-based promotion from QA to production

6. Secure AWS Access
   - GitHub OIDC used instead of long-lived AWS access keys
   - AWS role assumption for secure deployment to EKS
   - Kubernetes secrets managed via External Secrets Operator

7. Monitoring & Logging
   - Prometheus for metrics collection
   - Grafana for dashboards
   - Loki and Alloy for centralized log aggregation

## Security in CI/CD

This project explicitly implements DevSecOps best practices in GitHub Actions:

- Gitleaks scans for leaked secrets in source code
- Trivy scans filesystem and Docker images for vulnerabilities
- Checkov checks Kubernetes, Terraform, and Dockerfile security posture
- SonarQube enforces code quality gates
- SBOM generation for traceability and compliance
- GitHub OIDC for AWS authentication to avoid long-lived IAM keys
- Secrets stored in AWS Secrets Manager / Kubernetes secret integrations

## Key Highlights

- Automated CI/CD from QA to production
- Integrated security and code-quality checks in the deployment pipeline
- Eliminated long-lived AWS credentials in GitHub Actions using OIDC
- Centralized secret management for Kubernetes workloads
- Persistent storage for stateful workloads
- HTTPS-enabled application access with end-to-end observability
