# Fundamentals of Power Packed – AWS | Docker | Kubernetes | Terraform
### Detailed Interview Preparation Notes (Real-World Focus)

This document covers **core fundamentals with deep explanations**, **real production context**, and **clear differentiation**, designed for **Cloud / DevOps / Platform Engineer interviews**.

---

# ☁️ AWS FUNDAMENTALS

## 1. Security Groups vs NACLs

### Security Groups
- Act as **virtual firewalls** for EC2
- **Stateful** (return traffic automatically allowed)
- Applied at **instance level**
- Supports **allow rules only**

### NACLs (Network ACLs)
- Act at **subnet level**
- **Stateless** (explicit allow/deny both directions)
- Used for **network-wide controls**

**Interview tip:**  
> Use SGs for app-level security, NACLs for coarse network restrictions.

---

## 2. Designing Highly Available Architectures

Key principles:
- Multi-AZ deployment
- Load Balancers
- Auto Scaling Groups
- Stateless application design
- Database replication
- Health checks

**Example:**  
ALB → ASG (Multi-AZ) → RDS Multi-AZ

---

## 3. S3 vs EBS vs EFS – When to Use What

| Service | Use Case |
|------|------|
| **S3** | Object storage, backups, static content |
| **EBS** | Block storage for EC2 (databases, OS) |
| **EFS** | Shared file system for multiple EC2 |

---

## 4. Auto Scaling vs Load Balancing

- **Load Balancer**: Distributes traffic
- **Auto Scaling**: Adds/removes instances

👉 Used **together** for scalability + availability

---

## 5. IAM Users vs Roles

- **User**: Long-term identity (humans)
- **Role**: Temporary permissions (apps, EC2, EKS)

**Best practice:**  
> Prefer IAM Roles over Users for workloads.

---

## 6. Spot vs On-Demand vs Reserved Instances

- **On-Demand**: Flexible, expensive
- **Reserved**: Long-term, cost-effective
- **Spot**: Cheapest, interruptible

---

## 7. VPC Networking Fundamentals

- VPC → Subnets → Route Tables
- IGW → Internet access
- NAT → Private subnet outbound access
- Security Groups + NACLs

---

## 8. ALB vs NLB – When to Use Each

| ALB | NLB |
|--|--|
| Layer 7 (HTTP/HTTPS) | Layer 4 (TCP/UDP) |
| Path-based routing | Ultra low latency |
| Web apps, APIs | gRPC, WebSockets |

---

## 9. Securing S3 Buckets

- Block Public Access
- Bucket policies
- IAM policies
- Enable encryption
- Access logs

---

## 10. Cross-Account Access in AWS

- IAM Role in target account
- Trust relationship
- AssumeRole via STS

Used in:
- Multi-account architectures
- CI/CD pipelines

---

## 11. IAM Policy Evaluation Logic

Order:
1. Explicit Deny
2. Explicit Allow
3. Default Deny

⚠️ **Explicit Deny always wins**

---

## 12. EC2 Stop vs Terminate

- **Stop**: Instance preserved, EBS stays
- **Terminate**: Instance deleted, EBS removed (unless retained)

---

## 13. Disaster Recovery (RTO vs RPO)

- **RTO**: Time to restore service
- **RPO**: Data loss tolerance

DR Models:
- Backup & Restore
- Pilot Light
- Warm Standby
- Active-Active

---

## 14. AWS Backup vs Snapshots

- **Snapshot**: Resource-level backup
- **AWS Backup**: Centralized backup management

---

# 🐳 DOCKER FUNDAMENTALS

## 15. Image vs Container

- Image: Blueprint
- Container: Running instance

---

## 16. Reducing Docker Image Size

- Multi-stage builds
- Alpine images
- Remove package cache
- `.dockerignore`

---

## 17. Multi-Stage Builds – Why They Matter

- Separate build & runtime
- Smaller images
- Better security

---

## 18. Data Persistence in Containers

Options:
- Volumes
- Bind mounts
- Cloud storage

---

## 19. Docker Networking Basics

- Bridge
- Host
- Overlay

---

## 20. Why Avoid `latest` Tag in Production

- Unpredictable deployments
- Difficult rollbacks
- Version ambiguity

---

## 21. Why Containers Over VMs?

- Faster startup
- Lightweight
- Better resource utilization
- CI/CD friendly

---

## 22. Why Containers Exit?

- App crash
- Resource limits
- Signal termination
- Configuration error

---

## 23. CMD vs ENTRYPOINT

- ENTRYPOINT: Fixed executable
- CMD: Default arguments

---

## 24. Debugging Crashing Containers

- `docker logs`
- `docker exec`
- Check exit codes
- Inspect image

---

## 25. Docker Layer Caching

- Reuses unchanged layers
- Faster builds
- Ordering matters in Dockerfile

---

## 26. Image Vulnerability Scanning

Tools:
- Trivy
- Snyk
- ECR scanning
- Clair

---

# ☸️ KUBERNETES FUNDAMENTALS

## 27. Deployment vs StatefulSet vs DaemonSet

- Deployment: Stateless apps
- StatefulSet: Databases
- DaemonSet: Node-level agents

---

## 28. ClusterIP vs NodePort vs LoadBalancer

- ClusterIP: Internal
- NodePort: Node-level exposure
- LoadBalancer: Cloud-managed LB

---

## 29. Role of etcd

- Cluster state store
- Highly consistent key-value DB
- Critical for control plane

---

## 30. Pod Scheduling Process

1. Filter nodes
2. Score nodes
3. Bind pod

---

## 31. ConfigMap vs Secret

- ConfigMap: Non-sensitive
- Secret: Sensitive (base64 + encryption)

---

## 32. Liveness vs Readiness Probes

- Liveness: Restart pod
- Readiness: Control traffic

---

## 33. Metrics Server Usage

- Provides CPU & memory metrics
- Required for HPA

---

## 34. What Happens on `kubectl apply`

- Compare desired vs current state
- Patch changes
- Store config in etcd

---

## 35. Kubernetes Self-Healing

- Restart failed containers
- Reschedule pods
- Maintain desired state

---

## 36. HPA vs Cluster Autoscaler

- HPA: Scales pods
- CA: Scales nodes

---

## 37. Rolling Update Internals

- Create new ReplicaSet
- Gradual pod replacement
- Controlled by maxSurge/maxUnavailable

---

## 38. Kubernetes Namespace

- Logical isolation
- Resource management
- Access control

---

## 39. Secrets Management in Kubernetes

- Encrypted secrets
- External secret managers
- RBAC restrictions

---

## 40. Pod Affinity & Anti-Affinity

- Control pod placement
- Improve availability

---

## 41. Taints & Tolerations

- Taints repel pods
- Tolerations allow placement

---

# 🌍 TERRAFORM FUNDAMENTALS

## 42. Module vs Resource

- Resource: Single infra unit
- Module: Reusable infra block

---

## 43. Terraform State – Why It Matters

- Tracks real infrastructure
- Enables diff detection
- Required for updates & destroy

---

## 44. Managing Secrets Securely

- Environment variables
- Secret managers
- Avoid hardcoding

---

## 45. Terraform Plan vs Apply

- Plan: Preview changes
- Apply: Execute changes

---

## 46. Terraform Workflow

1. init
2. plan
3. apply
4. destroy

---

## 47. Managing State in a Team

- Remote backend (S3)
- State locking (DynamoDB)
- Access control

---

## 48. Remote Backends – Why Needed

- Collaboration
- Security
- Locking

---

## 49. Import Existing Infra

- `terraform import`
- Sync infra with state

---

## 50. count vs for_each

- count: Index-based
- for_each: Key-based (preferred)

---

## 51. Environment Separation (Dev/Stage/Prod)

- Separate workspaces
- Separate state files
- Separate variables

---

## 📌 FINAL INTERVIEW TIP

Always explain:
- **Why you chose a service**
- **How you handled failure**
- **What trade-offs you accepted**




