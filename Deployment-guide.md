This guide outlines all commands and steps used to deploy the EKS Fargate cluster and the AWS Load Balancer Controller.

1️⃣ **Create an EKS Cluster with Fargate**

eksctl create cluster --name my-cluster --region us-east-2 --fargate

**Update kubeconfig:**

aws eks update-kubeconfig --name my-cluster --region us-east-2
  
2️⃣ **Create a Fargate Profile for the Application**
- eksctl create fargateprofile --cluster my-cluster --region us-east-2 --name alb-sample-app --namespace game-2048
  
3️⃣ **Deploy the 2048 Sample Application**

- kubectl apply -f https://raw.githubusercontent.com/kubernetes-sigs/aws-load-balancer-controller/v2.5.4/docs/examples/2048/2048_full.yaml

4️⃣ Associate the IAM OIDC Provider

- eksctl utils associate-iam-oidc-provider --cluster my-cluster --approve
  
5️⃣ **Create IAM Policy for AWS Load Balancer Controller**

Download policy:
- curl -O https://raw.githubusercontent.com/kubernetes-sigs/aws-load-balancer-controller/v2.11.0/docs/install/iam_policy.json

Create IAM policy:

- aws iam create-policy --policy-name AWSLoadBalancerControllerIAMPolicy --policy-document file://iam_policy.json
  
6️⃣** Create IAM Service Account**

- eksctl create iamserviceaccount --cluster my-cluster --namespace kube-system --name aws-load-balancer-controller --role-name AmazonEKSLoadBalancerControllerRole --attach-policy-arn arn:aws:iam::<ACCOUNT_ID>:policy/AWSLoadBalancerControllerIAMPolicy --approve

7️⃣ Install AWS Load Balancer Controller (Helm)

**Add repo & update:**

- helm repo add eks https://aws.github.io/eks-charts
- helm repo update eks

**Install controller:**

- helm install aws-load-balancer-controller eks/aws-load-balancer-controller -n kube-system --set clusterName=my-cluster --set serviceAccount.create=false --set serviceAccount.name=aws-load-balancer-controller --set region=us-east-2 --set vpcId=<your-vpc-id>

**Verify:**

- kubectl get deployment -n kube-system aws-load-balancer-controller
