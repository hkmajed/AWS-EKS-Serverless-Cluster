# AWS-EKS-Serverless-Cluster

This project demonstrates the end-to-end deployment of a managed Kubernetes environment using Amazon EKS (Elastic Kubernetes Service). By utilizing a Fargate (serverless) profile, I removed the overhead of managing EC2 worker nodes, focusing instead on application delivery and automated scaling.
The architecture includes a fully configured AWS Load Balancer Controller, allowing Kubernetes Ingress resources to automatically provision and manage AWS Application Load Balancers (ALB).

🛠️ Key Technologies

- Orchestration: Amazon EKS (Kubernetes).
- Compute: AWS Fargate (Serverless).
- Networking: AWS Load Balancer Controller, Amazon VPC.
- Provisioning Tools: eksctl, kubectl, Helm.
- IAM Security: OIDC Identity Provider for fine-grained service account permissions.
