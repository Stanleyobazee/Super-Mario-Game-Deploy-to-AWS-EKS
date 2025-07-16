# Super Mario Game on AWS EKS

Deploy a classic Super Mario Bros game on Amazon Elastic Kubernetes Service (EKS) using Terraform and Kubernetes.

## 🎮 Project Overview

This project demonstrates how to deploy a containerized Super Mario game on AWS EKS cluster with Infrastructure as Code (IaC) using Terraform.

## 🏗️ Architecture

- **AWS EKS Cluster**: Managed Kubernetes service
- **VPC**: Custom VPC with public subnets across 2 AZs
- **Load Balancer**: AWS Application Load Balancer for external access
- **Container**: Super Mario game running in Docker containers

## 📁 Project Structure

```
Super-Mario-Game-Deploy-to-AWS-EKS/
├── EKS-TF/                 # Terraform configuration
│   ├── main.tf            # Main infrastructure resources
│   ├── provider.tf        # AWS provider configuration
│   ├── variables.tf       # Input variables
│   └── outputs.tf         # Output values
├── deployment.yml         # Kubernetes deployment manifest
├── service.yml           # Kubernetes service manifest
├── scripts.sh           # Installation script for tools
├── screenshots/         # Project screenshots
└── README.md           # This file
```

## 🚀 Prerequisites

- AWS CLI configured with appropriate permissions
- Terraform >= 1.0
- kubectl
- Docker (optional, for local testing)

## 📋 Quick Setup

### 1. Install Required Tools
```bash
chmod +x scripts.sh
./scripts.sh
```

### 2. Configure AWS Credentials
```bash
aws configure
```

### 3. Deploy Infrastructure
```bash
cd EKS-TF
terraform init
terraform plan
terraform apply
```

### 4. Configure kubectl
```bash
aws eks update-kubeconfig --region eu-north-1 --name eks-super-mario-game-cluster
```

### 5. Deploy Application
```bash
kubectl apply -f deployment.yml
kubectl apply -f service.yml
```

### 6. Get External URL
```bash
kubectl get service mario-service
```

## 🔧 Configuration Details

### Terraform Resources
- **VPC**: 10.0.0.0/16 with 2 public subnets
- **EKS Cluster**: Managed Kubernetes cluster
- **Node Group**: t3.medium instances (1-2 nodes)
- **IAM Roles**: Required permissions for EKS

### Kubernetes Resources
- **Deployment**: 2 replicas of Super Mario game
- **Service**: LoadBalancer type for external access
- **Container Image**: `sevenajay/mario:v1`

## 🎯 Access the Game

After deployment, get the external URL:
```bash
kubectl get service mario-service
```

Open the EXTERNAL-IP URL in your browser to play Super Mario!

## 🧹 Cleanup

```bash
# Delete Kubernetes resources
kubectl delete -f service.yml
kubectl delete -f deployment.yml

# Destroy infrastructure
cd EKS-TF
terraform destroy
```

## 📸 Screenshots

Screenshots of the deployment process and running game are stored in the `screenshots/` directory.

## 🛠️ Troubleshooting

### Common Issues

1. **ImagePullBackOff**: Check if the container image exists and is accessible
2. **Service not accessible**: Verify security groups and LoadBalancer configuration
3. **Terraform errors**: Ensure AWS credentials and permissions are correct

### Useful Commands
```bash
# Check pod status
kubectl get pods

# Describe pod for detailed info
kubectl describe pod <pod-name>

# Check service status
kubectl get services

# View logs
kubectl logs <pod-name>
```

## 📝 Variables

| Variable | Description | Default |
|----------|-------------|---------|
| aws_region | AWS region for deployment | eu-north-1 |
| project_name | Project name prefix | eks-super-mario-game |

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Submit a pull request

## 📄 License

This project is licensed under the MIT License - see the LICENSE file for details.

## 🎮 Enjoy the Game!

Once deployed, you can play the classic Super Mario Bros game directly in your browser!