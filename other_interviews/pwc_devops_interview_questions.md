# PwC DevOps Interview Questions & Answers
## Bash | Python | AWS | Git | CI/CD | Docker | Kubernetes | Terraform

This document contains **commonly discussed DevOps interview questions** for **PwC and similar consulting/product companies**, along with **clear, practical answers**.

---

## 🔹 Bash Scripting

### 1. Write a bash script to find the top 5 largest files in a directory.

```bash
#!/bin/bash
DIR=${1:-.}

find "$DIR" -type f -exec du -h {} + | sort -hr | head -5
Explanation:

find → finds files

du -h → file size
```

sort -hr → sort by size

head -5 → top 5 results

## 🔹 Python Scripting
## 2. Write a Python script to count how many times the word "ERROR" appears in a log file.
```text
def count_errors(file_path):
    count = 0
    with open(file_path, "r") as file:
        for line in file:
            if "ERROR" in line:
                count += 1
    return count

print(count_errors("app.log"))
```
Used in log analysis, monitoring, and alerting.

## 🔹 AWS
## 3. Difference between EC2, ECS, and EKS
Service	Description	When to Use
EC2	Virtual machines	Legacy / VM-based apps
ECS	AWS container service	Simple container workloads
EKS	Kubernetes on AWS	Standard Kubernetes platforms

## 4. Security Groups vs NACLs
Security Group	NACL
Stateful	Stateless
Instance-level	Subnet-level
Allow rules only	Allow & Deny

## 5. IAM Role vs IAM User
IAM User: Long-term credentials for humans

IAM Role: Temporary credentials for services (EC2, ECS, EKS)

Best practice: Always use roles for applications.

## 6. EC2 Stop vs Terminate
Stop: Instance stops, data preserved

Terminate: Instance deleted permanently

## 7. ALB vs NLB vs CLB
ALB	NLB	CLB
Layer 7	Layer 4	Legacy
HTTP/HTTPS	TCP/UDP	Not recommended
Path-based routing	High performance	Old generation

## 8. How Auto Scaling works with ALB
ALB distributes traffic

ASG scales instances based on CloudWatch metrics

Health checks remove unhealthy instances

## 9. What is VPC Peering & its limitations?
VPC Peering: Private connection between two VPCs.

Limitations:

No transitive routing

No overlapping CIDR

No centralized routing

## 10. Difference between S3 and EBS
S3	EBS
Object storage	Block storage
Highly durable	Attached to EC2
Backups, static files	OS, databases

## 🔹 Git
## 11. Git merge vs Git rebase
Merge: Preserves history

Rebase: Linear history, rewrites commits

## 12. How do you resolve merge conflicts?
Identify conflicting files

Edit conflict markers

git add

git commit

## 🔹 GitHub Actions
## 13. How does a GitHub Actions workflow get triggered?
Triggers include:

push

pull_request

workflow_dispatch

schedule

yaml
Copy code
on: [push]
## 14. Structure of GitHub Actions YAML
yaml
Copy code
name: CI
on: push
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - run: npm test
## 🔹 GitLab CI/CD
## 15. GitHub Actions vs GitLab CI/CD
GitHub Actions	GitLab CI
GitHub native	GitLab native
Marketplace actions	Built-in CI
YAML workflows	.gitlab-ci.yml

## 16. Stages & Jobs in GitLab
Stages: Pipeline phases

Jobs: Tasks in each stage

## 17. Structure of .gitlab-ci.yml
yaml
Copy code
stages:
  - build
  - deploy

build_job:
  stage: build
  script: mvn package
## 18. Artifacts vs Cache in GitLab
Artifacts: Stored outputs

Cache: Speeds up builds

## 19. How do GitLab runners work?
Execute CI jobs

Can be shared or specific

Run on VM, Docker, or Kubernetes

## 20. Protected branch & protected variable
Protected branch: Restricts pushes

Protected variable: Available only in protected branches

## 21. Manual pipeline trigger in GitLab
when: manual

## 🔹 Docker
## 22. Docker image vs container
Image → Blueprint

Container → Running instance

## 23. Multi-stage Docker build
Used to:

Reduce image size

Improve security

Separate build & runtime

## 🔹 Kubernetes
## 24. Deployment vs StatefulSet vs DaemonSet
Type	Use
Deployment	Stateless apps
StatefulSet	Databases
DaemonSet	Node agents

## 25. Rolling updates in Kubernetes
Gradual pod replacement

Controlled by maxSurge and maxUnavailable

## 26. Pod restarts & failures
Kubelet restarts containers

Repeated failures → CrashLoopBackOff

## 27. Node NotReady state
Causes:

Network issues

Disk pressure

Kubelet failure

## 28. ClusterIP vs NodePort vs LoadBalancer
ClusterIP → Internal access

NodePort → Node-level access

LoadBalancer → External access

## 29. Liveness vs Readiness probes
Liveness → Restart pod

Readiness → Control traffic

## 30. ConfigMaps vs Secrets
ConfigMap → Non-sensitive configs

Secret → Sensitive data

## 31. Horizontal Pod Autoscaler (HPA)
Uses metrics server

Scales pods automatically

## 32. Ingress vs Service
Service → Internal networking

Ingress → External HTTP routing

## 33. Kubernetes namespaces
Used for:

Environment isolation

RBAC

Resource quotas

## 34. Pod stuck in CrashLoopBackOff — troubleshooting
Check logs

Verify env variables

Check resource limits

Fix application error

## 🔹 Terraform
## 35. Terraform state file
- Tracks infrastructure
- Enables change detection
- Stored locally or remotely

## 36. terraform plan vs terraform apply
- plan: Preview changes
- apply: Create/update resources

## 📌 Final Interview Tip

## Always explain:
Concept
Real-world usage
Troubleshooting approach

### Author
**Velanati Naveen Kumar**
- DevOps Engineer  
- CI/CD | AWS | Kubernetes | Terraform | GitOps | Automation
- Connect with me: [LinkedIn](https://www.linkedin.com/in/naveenvelanati/)
- 📞 +91 9848545101
