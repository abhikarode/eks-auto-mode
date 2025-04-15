# EKS Auto Mode Terraform Project

This Terraform project creates an Amazon EKS cluster with Auto Mode enabled, along with all necessary supporting AWS resources.

## Features

- EKS cluster with Auto Mode enabled
- VPC with public, private, and intra subnets
- NAT Gateway for outbound internet access
- Proper tagging for EKS integration
- Admin permissions for the cluster creator

## Prerequisites

- Terraform >= 1.3.2
- AWS CLI configured with appropriate permissions
- kubectl (for interacting with the cluster after creation)

## Usage

1. Initialize the Terraform project:

```bash
terraform init
```

2. Review the planned changes:

```bash
terraform plan
```

3. Apply the configuration:

```bash
terraform apply
```

4. After successful creation, configure kubectl to interact with your cluster:

```bash
aws eks update-kubeconfig --name dev-q-eks-cluster --region us-west-2
```

5. Verify the cluster is working:

```bash
kubectl get nodes
```

## Testing Auto Mode

To test the auto-scaling capabilities of EKS Auto Mode, you can deploy a sample application:

```bash
kubectl apply -f sample-deployment.yaml
```

## Cleanup

To destroy all resources created by this project:

```bash
terraform destroy
```

## Architecture

- **VPC**: A dedicated VPC with CIDR block 10.0.0.0/16
- **Subnets**: 
  - Private subnets for EKS nodes
  - Public subnets for load balancers
  - Intra subnets for internal resources
- **EKS Cluster**: Running version 1.31 with Auto Mode enabled
- **Node Pools**: Using the default "general-purpose" node pool

## Notes on EKS Auto Mode

EKS Auto Mode extends AWS management beyond just the control plane to include:
- Automatic node provisioning and scaling
- Integrated load balancing
- Automated storage configuration
- Simplified networking
- Regular node replacement (max 21-day lifetime)

This eliminates the need to manually configure node groups, auto-scaling groups, or Karpenter.
