# AWS DevOps Interview Questions & Answers (Complete Guide)

A **production-grade AWS DevOps interview handbook** covering concepts, architecture, EKS, ECR, CI/CD, Terraform, and real hands-on projects.

---

## 📌 Table of Contents

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
14. High Availability & Disaster Recovery  
15. Cost Optimization  
16. Scenario-Based Interview Questions  
17. Architecture Diagrams  
18. Hands-On Projects  
19. GitHub Repository Structure  
20. How Interviewers Evaluate You  

---

## 1. AWS Fundamentals

### What is AWS?
AWS (Amazon Web Services) is a cloud computing platform offering on-demand compute, storage, networking, security, and managed services using a **pay-as-you-go** model.

### Advantages of AWS
- Elastic scalability
- High availability
- Global infrastructure
- Managed services
- Cost optimization

### Region vs Availability Zone
- **Region**: A geographical area (e.g., `us-east-1`)
- **AZ**: Isolated data centers within a region

---

## 2. IAM & Security

### What is IAM?
IAM (Identity and Access Management) controls **who can access what** in AWS.

### IAM User vs IAM Role

| IAM User | IAM Role |
|--------|---------|
| Permanent identity | Temporary credentials |
| Human access | Service/application access |
| Long-term keys | Uses STS |

### Least Privilege Principle
Grant **only the minimum permissions** required to perform a task.

### What is STS?
AWS Security Token Service provides **temporary, short-lived credentials**.

---

## 3. Compute Services

### What is EC2?
Elastic Compute Cloud provides resizable virtual machines.

### EC2 Instance Types
- General Purpose (t3, m5)
- Compute Optimized (c5)
- Memory Optimized (r5)
- Storage Optimized (i3)

### What is an AMI?
Amazon Machine Image is a template used to launch EC2 instances.

---

## 4. Storage Services

### What is Amazon S3?
Object storage for scalable, durable data storage.

### S3 Storage Classes
- Standard
- Intelligent-Tiering
- Standard-IA
- One Zone-IA
- Glacier
- Glacier Deep Archive

### What is EBS?
Block-level storage attached to EC2 instances.

---

## 5. Networking (VPC)

### What is VPC?
A logically isolated virtual network in AWS.

### Core VPC Components
- Subnets
- Route Tables
- Internet Gateway
- NAT Gateway
- Security Groups
- NACLs

### Security Group vs NACL

| Security Group | NACL |
|---------------|------|
| Stateful | Stateless |
| Instance-level | Subnet-level |
| Allow rules only | Allow & deny rules |

---

## 6. Load Balancing & Auto Scaling

### Load Balancer Types
- **ALB (Layer 7)** – HTTP/HTTPS routing
- **NLB (Layer 4)** – TCP/UDP traffic
- Classic Load Balancer (legacy)

### What is Auto Scaling?
Automatically adjusts EC2 capacity based on demand.

---

## 7. Databases

### AWS Database Services
- RDS (MySQL, PostgreSQL, Oracle)
- DynamoDB (NoSQL)
- Aurora
- Redshift

### Multi-AZ vs Read Replica
- **Multi-AZ** → High availability
- **Read Replica** → Read scalability

---

## 8. Monitoring & Logging

### Amazon CloudWatch
- Metrics
- Logs
- Alarms
- Dashboards

### AWS CloudTrail
Tracks **API calls** for auditing and security.

---

## 9. CI/CD & DevOps on AWS

### What is CI/CD?
- **CI**: Continuous Integration
- **CD**: Continuous Deployment / Delivery

### AWS DevOps Services
- CodeCommit
- CodeBuild
- CodeDeploy
- CodePipeline

### Jenkins on AWS
Jenkins can run on **EC2 or EKS** for CI pipelines.

---

## 10. Infrastructure as Code (IaC)

### What is IaC?
Managing infrastructure using code instead of manual configuration.

### Terraform vs CloudFormation

| Terraform | CloudFormation |
|---------|----------------|
| Multi-cloud | AWS only |
| HCL | JSON / YAML |
| Remote backend | Managed by AWS |

---

## 11. Containers on AWS

### What is Docker?
A container platform for packaging applications with dependencies.

### ECS vs EKS

| ECS | EKS |
|----|----|
| AWS native | Kubernetes |
| Simple setup | Advanced control |
| Limited flexibility | Full K8s ecosystem |

---

## 12. Amazon ECR (Elastic Container Registry)

### What is ECR?
A managed Docker image registry.

### ECR Features
- IAM authentication
- Image scanning
- Lifecycle policies
- Fully managed

### Push Image to ECR
1. Authenticate Docker
2. Build image
3. Tag image
4. Push to ECR

---

## 13. Amazon EKS (Elastic Kubernetes Service)

### What is EKS?
A managed Kubernetes service where AWS manages the **control plane**.

### Responsibility Model

| Component | Managed By |
|---------|------------|
| Control Plane | AWS |
| Worker Nodes | Customer |
| Networking | Shared |

### Node Types
- Managed Node Groups
- Self-managed Nodes
- AWS Fargate

### Authentication
- IAM + `aws-auth` ConfigMap
- Kubernetes RBAC

### Service Exposure
- ClusterIP
- NodePort
- LoadBalancer
- Ingress (ALB)

---

## 14. High Availability & Disaster Recovery

### HA Strategies
- Multi-AZ
- Auto Scaling
- Load Balancer

### DR Strategies
- Backup & Restore
- Pilot Light
- Warm Standby
- Active-Active

---

## 15. Cost Optimization

### Techniques
- Right sizing
- Reserved Instances
- Spot Instances
- Auto Scaling
- S3 lifecycle policies

### Cost Tools
- Cost Explorer
- Budgets
- Trusted Advisor

---

## 16. Scenario-Based Questions

### HA Web App Design
- ALB
- Auto Scaling Group
- Multi-AZ RDS
- CloudWatch

### Secure EKS
- Private endpoint
- IRSA
- Network policies
- Secrets Manager

### CI/CD for EKS
- Jenkins / GitHub Actions
- Docker + ECR
- ArgoCD (GitOps)

---

## 17. Architecture Diagrams

### 17.1 Highly Available Web Application

```text
Users
  |
Route 53
  |
ALB (Layer 7)
  |
EC2 (AZ-1) ---- EC2 (AZ-2)
        |
     RDS (Multi-AZ)
