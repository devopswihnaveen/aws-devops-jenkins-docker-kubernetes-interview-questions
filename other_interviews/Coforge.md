# Coforge – DevOps / Cloud / Kubernetes Interview Preparation (Detailed)

This document provides **in-depth explanations**, **real production context**, and **best-practice answers** for DevOps, Kubernetes, Cloud, CI/CD, and Terraform interviews.

---

## 1. Explain your CI/CD pipeline end to end.

Our CI/CD pipeline follows a **fully automated DevSecOps approach**:

### CI (Continuous Integration)
1. Developer pushes code to GitHub
2. Webhook triggers pipeline (Jenkins / GitHub Actions / GitLab CI)
3. Code checkout
4. Static code analysis (SonarQube)
5. Security scans (SAST, dependency check)
6. Build artifact or Docker image
7. Run unit & integration tests
8. Push image to registry (ECR)

### CD (Continuous Deployment)
9. Helm chart update or GitOps repo update
10. ArgoCD / Jenkins deploys to Kubernetes
11. Rolling / Canary deployment
12. Post-deployment health checks
13. Monitoring & alerts enabled

This ensures **fast, safe, repeatable releases**.

---

## 2. How do you handle zero-downtime deployments in Kubernetes?

Zero downtime is achieved by:
- Multiple replicas
- Readiness probes
- Rolling updates or Canary deployment
- Kubernetes Service abstraction

Traffic is routed only to **ready pods**.  
If failure occurs, we **rollback immediately using Helm or GitOps**.

---

## 3. Pod is running but service is unreachable – troubleshooting steps.

1. Check pod status & logs
2. Verify Service selector matches pod labels
3. Check service endpoints
4. Validate container port vs service port
5. Check NetworkPolicies
6. Verify security groups / NACLs
7. Test inside cluster using curl

---

## 4. How do you manage secrets securely in AWS / GCP / Azure?

Best practice:
- AWS Secrets Manager / SSM Parameter Store
- GCP Secret Manager
- Azure Key Vault
- External Secrets Operator in Kubernetes
- IAM-based access

Secrets are **never hardcoded or committed to Git**.

---

## 5. How do you design a scalable architecture for high-traffic apps?

Key principles:
- Stateless services
- Load balancers
- Auto Scaling Groups / HPA
- Caching (Redis)
- Async processing (SQS/Kafka)
- Multi-AZ deployment
- Database read replicas

This ensures **horizontal scalability & resilience**.

---

## 6. Common reasons for node pressure in Kubernetes.

- CPU exhaustion
- Memory leaks
- Disk usage
- Too many pods per node
- Incorrect resource requests/limits

Solved by:
- Resource tuning
- Node auto-scaling
- Pod eviction policies

---

## 7. How do you secure Kubernetes end-to-end?

- RBAC
- Network Policies
- Pod Security Standards
- Secrets encryption
- TLS (mTLS)
- Image scanning
- Audit logging
- Private API server access

---

## 8. ECR vs Docker Hub (real usage).

### Amazon ECR
- IAM-based authentication
- Private by default
- VPC endpoint support
- Enterprise security

### Docker Hub
- Public registry
- Rate limits
- External auth

**Production workloads prefer ECR**.

---

## 9. What happens if Terraform apply fails midway?

- Terraform updates state for completed resources
- Failed resources remain unmanaged
- Fix issue → re-run `terraform apply`
- Manual cleanup if resource partially created

State consistency is critical.

---

## 10. How do you debug a failing Helm release?

- `helm status <release>`
- `helm history`
- `kubectl describe pod`
- Check logs & events
- Rollback if needed

---

## 11. Git rebase vs Git merge.

- **Merge**: Keeps full history, safer for shared branches
- **Rebase**: Clean linear history, avoid on shared branches

---

## 12. Managing environment-specific variables in CI/CD.

- Separate values files
- Environment variables
- Secret managers
- Branch-based configs

---

## 13. Impact of using hostPath volumes.

- Node-dependent
- Security risk
- Not portable
- Avoid in production

---

## 14. What happens internally when GitHub triggers pipeline?

- Webhook event
- CI tool receives payload
- Pipeline execution
- Build → test → deploy

---

## 15. Lifecycle of a Pod.

1. Pending
2. Running
3. Succeeded / Failed
4. CrashLoopBackOff (if restarting)

---

## 16. Tracking configuration drift.

- Terraform plan
- Drift detection tools
- GitOps enforcement
- Scheduled audits

---

## 17. StatefulSet vs Deployment.

- Deployment → stateless apps
- StatefulSet → databases, stable identity, persistent storage

---

## 18. Logging design for microservices.

- Centralized logging
- Fluent Bit / Fluentd
- ELK / OpenSearch
- Correlation IDs

---

## 19. IAM User vs Role vs Policy.

- User → permanent identity
- Role → temporary permissions
- Policy → permission rules

---

## 20. Cloud cost optimization.

- Right-sizing
- Auto Scaling
- Spot instances
- Reserved Instances
- Storage lifecycle rules

---

## 21. How service meshes work (Istio/Linkerd).

- Sidecar proxies
- Traffic routing
- mTLS security
- Observability
- Policy control

---

## 22. High CPU usage troubleshooting.

- Check metrics
- Increase limits
- Scale pods
- Optimize application code

---

## 23. Handling pipeline secrets.

- CI secret vaults
- Masked variables
- IAM roles
- Rotation policies

---

## 24. Canary deployment example.

Deploy new version to 5% users → monitor → increase traffic → full rollout or rollback.

---

## 25. Helm versioning & rollback.

- Semantic versioning
- Helm history
- `helm rollback`

---

## 26. Dead Letter Queue (DLQ).

Stores failed messages.
Used in:
- SQS
- Kafka
- Event-driven systems

---

## 27. HPA autoscaling.

- Metrics server
- CPU/memory targets
- Automatic scaling

---

## 28. Blue-Green deployment & limitations.

- Instant switch
- Fast rollback
- Avoid when DB schema incompatible

---

## 29. Load testing before production.

- JMeter / k6
- Stress & spike tests
- Bottleneck identification

---

## 30. Terraform state file protection.

- Remote backend (S3)
- Encryption
- DynamoDB locking
- Restricted access

---

## 31. Production issue example.

Issue: High latency due to DB overload  
Fix:
- Monitoring
- Read replicas
- Caching

---

## 32. Docker image optimization.

- Multi-stage builds
- Smaller base images
- Remove unused layers

---

## 33. Rollback strategy.

- Helm rollback
- GitOps revert
- Blue-Green switch

---

## 34. Monitoring microservices.

- Metrics (Prometheus)
- Logs (ELK)
- Tracing (Jaeger)
- Alerts

---

## 35. Readiness vs Liveness probes.

- Readiness → traffic control
- Liveness → restart decision

---

## 36. Jenkins pipeline failure scenario.

Failure due to disk exhaustion.
Fix:
- Cleanup workspace
- Add disk monitoring
- Pipeline optimization

---

## 37. Handling Terraform drift.

- Plan reviews
- Re-apply from Git
- Avoid manual changes

---

## 38. Blue-Green vs Rolling deployment.

- Blue-Green → instant switch
- Rolling → gradual update

---

## 39. VPC, Subnets, Route Tables, NAT & IGW.

- VPC → virtual network
- Subnet → network segmentation
- Route table → traffic rules
- IGW → internet access
- NAT → outbound internet for private subnets

---

## 📌 Final Tip
Always explain:
- **Why you chose a design**
- **How you handled failures**
- **What you improved after incidents**

---

### Author
DevOps / Cloud Engineer  
AWS | Kubernetes | CI/CD | Terraform | Microservices
