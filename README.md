# Project-Bedrock

Project Bedrock – InnovateMart EKS Deployment

Author: Grace Ikpang – Cloud DevOps Engineer
Institution: Altschool Africa – 3rd Semester Assessment

Introduction

This project documents the deployment of the Retail Store Sample Application to Amazon Elastic Kubernetes Service (EKS). Infrastructure was provisioned using Terraform, the application was deployed to the cluster, and exposed through an AWS Application Load Balancer (ALB) using Kubernetes Ingress.

Demo Store: http://aea3412764bd5427186c0b6709b40507-1612858443.eu-west-2.elb.amazonaws.com/

Repository: https://github.com/GraceIkpang/Project-Bedrock

1. Infrastructure Provisioning

Provisioned AWS resources with Terraform.

Resources defined in .tf files for clarity and maintainability:

VPC and subnets

Internet Gateway and route tables

EKS cluster and managed node groups

IAM roles and policies for cluster and nodes

Configured a remote backend to securely store Terraform state.

2. EKS Cluster Setup

Deployed EKS cluster in eu-west-2 region.

Configured worker nodes with auto-scaling enabled.

Updated local kubeconfig for cluster access:

aws eks update-kubeconfig --name <cluster-name> --region eu-west-2

3. Application Deployment

Deployed the retail-store-sample-app into the retail-dev namespace.

Kubernetes resources included:

Deployments for frontend UI and backend API services

Services for internal communication (ClusterIP)

Verified that all pods were running successfully.

4. Ingress & Load Balancing

Installed and configured the AWS Load Balancer Controller.

Created an Ingress resource to expose the application externally.

Configured internet-facing ALB with listeners on ports 80/443 and health checks for services.

5. CI/CD Pipeline

Implemented a GitHub Actions workflow (terraform.yaml) located under .github/workflows/.

The workflow automates Terraform operations as follows:

On feature branch push: runs terraform fmt, terraform validate, and terraform plan.

On merge to main: executes terraform apply to provision or update infrastructure.

AWS credentials were configured using GitHub Secrets to avoid hardcoding.

6. Developer Access (Read-Only)

Provisioned an IAM user with limited permissions.

Integrated with Kubernetes RBAC to allow developers to:

List and describe pods

View logs

Check service status

Access steps documented for switching kubeconfig context with --profile dev-readonly.

7. Challenges

Encountered pod failures due to insufficient instance size.

Resolved by resizing worker nodes while staying within AWS free tier limits.

Conclusion

The project achieved its objectives by:

Provisioning AWS infrastructure via Terraform

Deploying a containerized application to EKS

Exposing the application through an ALB using Ingress

Automating deployments with a GitHub Actions pipeline

Configuring a secure read-only developer access model

This deployment demonstrates a production-ready foundation for cloud-native applications and provides a strong base for future improvements such as SSL, managed databases, and advanced monitoring.
