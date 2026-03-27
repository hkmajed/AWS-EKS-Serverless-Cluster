AWS EKS Serverless Cluster (Fargate)

This project demonstrates how to deploy a serverless Kubernetes environment using Amazon EKS with AWS Fargate as the compute engine.
It also includes the installation of the AWS Load Balancer Controller, which enables Kubernetes Ingress resources to automatically provision and manage Application Load Balancers (ALB).

The deployment is fully automated using eksctl, kubectl, the AWS CLI, and Helm.

🚀 Features
Fully managed EKS control plane
Serverless compute using AWS Fargate (no EC2 worker nodes)
Ingress support using AWS Load Balancer Controller
Automatic provisioning of Application Load Balancers (ALB)
IAM roles mapped to Kubernetes using OIDC connector
Deployment of a sample app (2048 game)

🛠️ Tools & Technologies
Category	Technology
Orchestration	Amazon EKS (Kubernetes)
Compute	AWS Fargate
Networking	AWS Load Balancer Controller, ALB, VPC
Provisioning	eksctl, kubectl, AWS CLI, Helm
IAM	IAM OIDC Provider, IAM Service Accounts

📦 Project Structure

AWS-EKS-Fargate-Cluster/
│
├── README.md               # Project overview (this file)
└── deployment-guide.md     # All steps and commands needed to reproduce the setup
