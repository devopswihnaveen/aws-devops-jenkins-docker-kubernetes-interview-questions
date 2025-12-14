# AWS DevOps Interview Questions & Answers (Complete Guide)

## Table of Contents
1. AWS Fundamentals  
2. IAM & Security  
3. Compute Services  
4. Storage Services  
5. Networking (VPC)  
6. Load Balancing & Auto Scaling  
7. Databases  
8. Monitoring & Logging  
9. CI/CD & DevOps on AWS  
10. Infrastructure as Code (IaC)  
11. Containers on AWS  
12. Amazon ECR  
13. Amazon EKS  
14. High Availability & DR  
15. Cost Optimization  
16. Scenario-Based Interview Questions  

---

## 1. AWS Fundamentals

### What is AWS?
AWS (Amazon Web Services) is a cloud platform providing on-demand compute, storage, networking, security, and managed services on a pay-as-you-go model.

### What are the advantages of AWS?
- Scalability
- High availability
- Pay-as-you-go pricing
- Global infrastructure
- Managed services

### What is a Region and AZ?
- **Region**: A geographical area (e.g., us-east-1)
- **Availability Zone (AZ)**: Isolated data centers within a region

---

## 2. IAM & Security

### What is IAM?
IAM (Identity and Access Management) allows you to manage users, roles, groups, and permissions.

### Difference between IAM User and Role?
| IAM User | IAM Role |
|--------|---------|
| Permanent identity | Temporary credentials |
| Used by humans | Used by services/apps |
| Long-term access keys | Uses STS |

### What is least privilege?
Granting only minimum permissions required to perform a task.

### What is STS?
AWS Security Token Service provides temporary credentials for secure access.

---

## 3. Compute Services

### What is EC2?
Elastic Compute Cloud provides resizable virtual machines.

### EC2 instance types?
- General Purpose (t3, m5)
- Compute Optimized (c5)
- Memory Optimized (r5)
- Storage Optimized (i3)

### What is AMI?
Amazon Machine Image is a template used to launch EC2 instances.

---

## 4. Storage Services

### What is S3?
Simple Storage Service is an object storage service.

### S3 Storage Classes?
- Standard
- IA
- One Zone-IA
- Glacier
- Glacier Deep Archive

### What is EBS?
Elastic Block Store provides block-level storage for EC2.

---

## 5. Networking (VPC)

### What is VPC?
Virtual Private Cloud is a logically isolated network in AWS.

### Components of VPC?
- Subnets
- Route Tables
- Internet Gateway
- NAT Gateway
- Security Groups
- NACLs

### Security Group vs NACL?
| Security Group | NACL |
|--------------|------|
| Stateful | Stateless |
| Instance-level | Subnet-level |
| Allow rules only | Allow & deny |

---

## 6. Load Balancing & Auto Scaling

### Types of Load Balancers?
- ALB (Layer 7)
- NLB (Layer 4)
- Classic LB

### What is Auto Scaling?
Automatically increases or decreases EC2 instances based on demand.

---

## 7. Databases

### Types of AWS Databases?
- RDS (MySQL, PostgreSQL, Oracle)
- DynamoDB (NoSQL)
- Aurora
- Redshift

### Multi-AZ vs Read Replica?
- **Multi-AZ**: High availability
- **Read Replica**: Read scalability

---

## 8. Monitoring & Logging

### What is CloudWatch?
Monitoring service for metrics, logs, and alarms.

### What is CloudTrail?
Records API calls for auditing and security.

---

## 9. CI/CD & DevOps on AWS

### What is CI/CD?
- CI: Continuous Integration
- CD: Continuous Deployment/Delivery

### AWS DevOps Tools?
- CodeCommit
- CodeBuild
- CodeDeploy
- CodePipeline

### Jenkins on AWS?
Jenkins can be hosted on EC2 or EKS for CI pipelines.

---

## 10. Infrastructure as Code (IaC)

### What is IaC?
Managing infrastructure using code.

### Terraform vs CloudFormation?
| Terraform | CloudFormation |
|---------|----------------|
| Multi-cloud | AWS-only |
| HCL | JSON/YAML |
| State file | Managed by AWS |

---

## 11. Containers on AWS

### What is Docker?
Containerization platform for packaging applications.

### ECS vs EKS?
| ECS | EKS |
|----|----|
| AWS native | Kubernetes |
| Simple | Complex |
| Less control | Full K8s control |

---

## 12. Amazon ECR (Elastic Container Registry)

### What is ECR?
Managed Docker container registry to store, manage, and deploy images.

### ECR Features?
- Fully managed
- IAM-based authentication
- Image scanning
- Lifecycle policies

### Push image to ECR (Steps)?
1. Authenticate Docker to ECR
2. Build Docker image
3. Tag image
4. Push image to ECR

---

## 13. Amazon EKS (Elastic Kubernetes Service)

### What is EKS?
Managed Kubernetes service where AWS manages the control plane.

### Who manages what in EKS?
| Component | Managed By |
|--------|------------|
| Control Plane | AWS |
| Worker Nodes | Customer |
| Add-ons | Shared |

### EKS Node Types?
- Managed Node Groups
- Self-managed nodes
- Fargate

### How does EKS authentication work?
- IAM + aws-auth ConfigMap
- RBAC inside Kubernetes

### How to expose app in EKS?
- ClusterIP
- NodePort
- LoadBalancer
- Ingress (ALB)

---

## 14. High Availability & Disaster Recovery

### HA Strategies?
- Multi-AZ
- Load Balancer
- Auto Scaling

### DR Strategies?
- Backup & Restore
- Pilot Light
- Warm Standby
- Multi-site Active-Active

---

## 15. Cost Optimization

### AWS Cost Optimization Techniques?
- Right sizing
- Reserved Instances
- Spot Instances
- Auto Scaling
- S3 lifecycle policies

### AWS Cost Tools?
- Cost Explorer
- Budgets
- Trusted Advisor

---

## 16. Scenario-Based Interview Questions

### How do you deploy a highly available web app?
- ALB
- Auto Scaling Group
- Multi-AZ RDS
- CloudWatch monitoring

### How to secure EKS cluster?
- Private endpoint
- IAM roles for service accounts
- Network policies
- Secrets Manager

### How to design CI/CD for EKS?
- GitHub/Jenkins for CI
- Docker build
- Push to ECR
- ArgoCD for CD

---

## Final Notes
This document is designed for:
- AWS DevOps interviews
- Cloud Engineer roles
- SRE & Platform Engineer roles

⭐ Tip: Add diagrams and hands-on projects to strengthen interviews.
