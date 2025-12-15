# AWS | Docker | Kubernetes | Terraform  
## Interview Questions with Causes & Troubleshooting (Power-Packed)

This document explains **core DevOps interview questions** using a **cause-based and troubleshooting-oriented approach**, reflecting real production scenarios.

---

# 🔥 AWS

## 1. Difference between Security Groups and NACLs

### Cause / Concept
- **Security Groups (SG):** Instance-level firewall
- **NACLs:** Subnet-level firewall

### Key Difference
| Security Group | NACL |
|--------------|------|
| Stateful | Stateless |
| Allow rules only | Allow + Deny |
| Applied to EC2 | Applied to subnet |

### Troubleshooting Scenario
❌ Application not reachable  
✅ Check:
1. SG inbound rules
2. NACL inbound **and outbound** rules
3. Correct subnet association

---

## 2. Designing a Highly Available Architecture in AWS

### Cause
Single AZ deployments fail during AZ outages.

### Best Practice Design
- Multi-AZ subnets
- Load Balancer
- Auto Scaling Group
- Stateless app design
- Multi-AZ RDS

### Troubleshooting
1. Verify instances across AZs
2. Check health checks
3. Confirm failover configuration

---

## 3. When to Use S3 vs EFS vs EBS

### Cause
Wrong storage choice causes latency, data loss, or scaling issues.

| Service | Use Case |
|------|------|
| S3 | Object storage, backups |
| EBS | EC2 block storage |
| EFS | Shared file system |

### Troubleshooting
- Shared access needed → **EFS**
- DB / OS storage → **EBS**
- Static files → **S3**

---

## 4. Auto Scaling vs Load Balancing

### Cause
Confusion between scaling and traffic distribution.

- **Load Balancer:** Distributes traffic
- **Auto Scaling:** Adds/removes instances

### Troubleshooting
If app is slow:
1. Check LB metrics
2. Check ASG scaling policies

---

## 5. IAM Roles vs IAM Users

### Cause
Using IAM users for applications (security risk).

| IAM User | IAM Role |
|-------|---------|
| Long-term creds | Temporary creds |
| For humans | For services |

### Troubleshooting
❌ AccessDenied errors  
✅ Check:
- Role attached
- Trust relationship
- Policy permissions

---

## 6. Spot vs On-Demand vs Reserved Instances

### Cause
Unexpected EC2 termination or high cost.

| Type | Use |
|----|----|
| On-Demand | Flexible |
| Reserved | Cost saving |
| Spot | Cheapest, interruptible |

### Troubleshooting
- Spot terminated → check interruption notice
- Critical workload → avoid Spot

---

## 7. AWS VPC Networking Fundamentals

### Cause
Networking misconfiguration breaks connectivity.

### Components
- VPC
- Subnets
- Route Tables
- IGW (internet)
- NAT (private subnet outbound)

### Troubleshooting
1. Check route table
2. Check IGW/NAT
3. Check SG & NACL

---

# 🐳 Docker

## 8. Image vs Container

### Cause
Confusion between build-time and runtime.

- **Image:** Blueprint
- **Container:** Running instance

### Troubleshooting
Container exits → inspect image CMD/ENTRYPOINT

---

## 9. Reducing Docker Image Size

### Cause
Large images slow CI/CD and increase attack surface.

### Solutions
- Multi-stage builds
- Minimal base images
- `.dockerignore`
- Remove package cache

---

## 10. Docker Multi-Stage Build

### Cause
Build tools included in runtime image.

### Solution
Separate build & runtime stages.

### Benefit
- Smaller image
- Better security

---

## 11. Persisting Data in Containers

### Cause
Data loss on container restart.

### Solutions
- Docker volumes
- Bind mounts
- External storage (EBS/EFS)

---

## 12. Docker Networking Basics

### Cause
Containers cannot communicate.

### Types
- Bridge (default)
- Host
- Overlay (Swarm/K8s)

### Troubleshooting
1. Check network type
2. Check exposed ports

---

## 13. Why Avoid `latest` Tag in Production

### Cause
Unpredictable deployments.

### Problems
- No version control
- Hard rollback

### Best Practice
Use semantic versioning.

---

# ☸️ Kubernetes

## 14. Deployment vs StatefulSet vs DaemonSet

### Cause
Wrong controller choice.

| Type | Use |
|----|----|
| Deployment | Stateless apps |
| StatefulSet | Databases |
| DaemonSet | Node-level agents |

---

## 15. ClusterIP vs NodePort vs LoadBalancer

### Cause
Service not accessible.

| Type | Access |
|----|----|
| ClusterIP | Internal |
| NodePort | Node IP |
| LoadBalancer | External |

---

## 16. Role of etcd

### Cause
Cluster state corruption.

### Function
- Stores all cluster data
- Highly consistent KV store

### Troubleshooting
- etcd failure → cluster unavailable

---

## 17. Pod Scheduling Process

### Cause
Pods stuck in Pending.

### Steps
1. Filter nodes
2. Score nodes
3. Bind pod

### Troubleshooting
- Check resources
- Check taints/tolerations

---

## 18. ConfigMap vs Secret

### Cause
Sensitive data exposed.

| ConfigMap | Secret |
|---------|-------|
| Non-sensitive | Sensitive |
| Plain text | Base64 + encrypted |

---

## 19. Liveness vs Readiness Probes

### Cause
Traffic sent to unhealthy pods.

- **Liveness:** Restart pod
- **Readiness:** Control traffic

---

## 20. Kubernetes Metrics Server

### Cause
HPA not working.

### Purpose
- Provides CPU/memory metrics

### Troubleshooting
- Check metrics-server deployment

---

# 🧱 Terraform

## 21. Module vs Resource

### Cause
Code duplication.

- **Resource:** Single infra object
- **Module:** Reusable infra block

---

## 22. Terraform State – Why It Matters

### Cause
Terraform doesn’t know real infra state.

### Purpose
- Tracks resources
- Enables diff detection

---

## 23. Managing Secrets in Terraform

### Cause
Secrets leaked in Git.

### Solutions
- Environment variables
- Secret managers
- Never hardcode

---

## 24. Terraform Plan vs Apply

| Command | Purpose |
|------|-------|
| plan | Preview |
| apply | Execute |

---

## 25. Terraform Multi-Environment Setup

### Cause
Prod resources created in dev.

### Best Practices
- Separate state files
- Separate variable files
- Workspaces or directories

---

## 📌 FINAL INTERVIEW TIP

Always explain:
1. **Root cause**
2. **Impact**
3. **How you fixed it**
4. **How you prevented it**

---

### Author
**Velanati Naveen Kumar**  
DevOps Engineer  
CI/CD | AWS | Kubernetes | Terraform | GitOps | Automation  
📞 +91 9848545101
