# DevOps & Kubernetes Interview Questions – Real-World Answers

This repository contains **commonly asked DevOps, Kubernetes, Cloud, CI/CD, Docker, Terraform, and AWS interview questions** with **practical, production-focused answers**.

---

## 1. How do you design a zero-downtime deployment strategy in Kubernetes?

Zero-downtime deployments are achieved using:
- Multiple replicas
- Kubernetes Services
- Readiness & liveness probes
- Rolling updates, Blue-Green, or Canary deployments

Traffic is routed only to healthy pods, ensuring no service disruption.

---

## 2. Explain Blue-Green vs Canary deployment – when would you choose each?

**Blue-Green Deployment**
- Two identical environments (Blue = current, Green = new)
- Traffic switch happens instantly
- Fast rollback

**Canary Deployment**
- New version released to a small % of users
- Gradual rollout based on metrics

**Use Blue-Green** for risky releases  
**Use Canary** for continuous experimentation

---

## 3. What was your biggest production incident and how did you fix it?

A memory leak caused frequent pod restarts.
- Detected via Prometheus metrics
- Rolled back the deployment
- Fixed memory leak
- Added memory limits and alerts

---

## 4. How do you optimize Docker image size in real applications?

- Multi-stage builds
- Alpine or distroless images
- Remove unused dependencies
- Combine RUN commands
- Use `.dockerignore`

---

## 5. What metrics do you monitor in CI/CD pipelines to measure success?

- Deployment frequency
- Lead time for changes
- Change failure rate
- Mean Time To Recovery (MTTR)
- Pipeline success rate

---

## 6. How do you manage secrets across multiple environments securely?

- Kubernetes Secrets (encrypted)
- AWS Secrets Manager / HashiCorp Vault
- IAM roles instead of static credentials
- Never hardcode secrets

---

## 7. What happens in Kubernetes when a pod crashes?

- Kubelet restarts the container
- If repeated failures → `CrashLoopBackOff`
- Deployment ensures desired replica count

---

## 8. Explain step-by-step how you enabled auto-scaling for an application.

- Install Metrics Server
- Configure HPA using CPU/memory
- Tune thresholds

**Challenges**: Cold starts, incorrect thresholds

---

## 9. How do you automate infrastructure rollback in case of failure?

- Terraform rollback using state
- Helm rollback
- GitOps rollback via ArgoCD

---

## 10. How do you handle Terraform state file conflicts in a team?

- Remote backend (S3)
- DynamoDB state locking
- Separate workspaces
- Avoid manual changes

---

## 11. How do you secure your Jenkins pipeline?

- Role-based access control
- Secure credentials store
- Least privilege
- Webhook authentication
- Disable script console

---

## 12. What strategy do you use to reduce cost on AWS?

- Right-size EC2
- Spot instances
- Auto-scaling
- Reserved Instances
- S3 lifecycle policies

---

## 13. How do you handle long-running jobs in Kubernetes?

- Use Jobs or CronJobs
- Message queues (SQS, Kafka)
- Avoid blocking web pods

---

## 14. How do you debug a failed deployment in production?

- Check pod logs and events
- Compare configs
- Rollback immediately
- Validate environment variables

---

## 15. What is the difference between ClusterIP, NodePort, and LoadBalancer?

- **ClusterIP**: Internal communication
- **NodePort**: Exposes via node IP
- **LoadBalancer**: External access (AWS ALB/NLB)

---

## 16. Explain how service discovery works in microservices.

- Kubernetes DNS
- Service names resolve to cluster IPs
- Enables seamless microservice communication

---

## 17. How do you detect and stop a memory leak in a container?

- Monitor memory usage trends
- Heap dumps
- Set memory limits
- Restart policies

---

## 18. What’s your approach to disaster recovery planning?

- Multi-AZ / Multi-region
- Automated backups
- Define RTO & RPO
- Regular DR testing

---

## 19. How do you handle environment drift in Infrastructure as Code?

- Git as source of truth
- Terraform plan validation
- Drift detection tools

---

## 20. How do you integrate security checks inside CI/CD?

- SAST & DAST
- Image scanning
- Secrets scanning
- Policy enforcement

---

## 21. How do you implement multi-region deployment in AWS?

- Route53 latency routing
- Data replication
- Active-Active or Active-Passive setup

---

## 22. Explain IAM roles vs policies.

- **Policy** defines permissions
- **Role** assigns permissions to entities
Used extensively in automation and EKS

---

## 23. How do you monitor container performance?

- Prometheus
- Grafana dashboards
- Alertmanager alerts

---

## 24. What’s your approach to managing Terraform modules?

- Reusable modules
- Versioning
- Separate state per team/environment

---

## 25. How do you troubleshoot a pod stuck in ImagePullBackOff?

- Check image name & tag
- Verify registry credentials
- Network connectivity issues

---

## 26. Explain how you use Helm in real projects.

- Package Kubernetes manifests
- Environment-specific values
- Easy rollbacks
- Version control

---

## 27. How do you handle CI/CD for microservices?

- Independent pipelines
- Versioned Docker images
- Canary or rolling deployments

---

## 28. What checks do you include before merging code into production?

- Unit tests
- Linting
- Security scans
- Code reviews

---

## 29. Explain how you set up centralized logging.

- Fluentd / Fluent Bit
- ELK or OpenSearch
- Correlation IDs for tracing

---

## 30. How do you secure Kubernetes cluster communication?

- TLS encryption
- Network policies
- RBAC
- IAM for EKS

---

## 31. Difference between ReplicaSet and Deployment?

- ReplicaSet maintains pod count
- Deployment manages ReplicaSets and rollouts

---

## 32. How do you debug slow API responses?

- Latency metrics
- Logs & tracing
- Database query analysis
- Load testing

---

## 33. Why are sidecar containers used?

- Logging
- Service mesh proxies
- Security agents

---

## 34. How do you manage environment variables securely in Kubernetes?

- Secrets
- ConfigMaps
- External secret managers

---

## 35. What challenges have you faced while scaling Jenkins?

- Resource bottlenecks
- Solved using Kubernetes agents
- Shared pipeline libraries

---

## 36. How do you use AWS CloudWatch for proactive alerting?

- Alarms
- Anomaly detection
- EventBridge automation

---

## 37. How do you reduce Docker image layers?

- Combine RUN commands
- Remove cache
- Multi-stage builds

---

## 38. What is your strategy for patch management?

- AMI updates
- Rolling deployments
- Automated pipelines

---

## 39. How do you perform Blue-Green deployment using Load Balancer?

- Two target groups
- Switch traffic at LB level
- Instant rollback capability

---

## 📌 Author
**Cloud / DevOps Engineer**  
Focused on Kubernetes, AWS, Terraform, CI/CD, and production-grade automation.

---

⭐ If this helped you, star the repo and share with fellow DevOps engineers!

## 📁 Detailed Topic-Wise Resources

Each topic has been expanded into dedicated markdown files for in-depth learning:

- **[Kubernetes Deployments](./topics/kubernetes-deployments.md)** – Zero-downtime strategies, Blue-Green, Canary, Rolling updates
- **[Docker Optimization](./topics/docker-optimization.md)** – Image size reduction, multi-stage builds, best practices
- **[CI/CD Pipelines](./topics/cicd-pipelines.md)** – Jenkins security, metrics, automation, failure handling
- **[AWS & Cloud](./topics/aws-cloud.md)** – IAM, CloudWatch, multi-region, cost optimization
- **[Kubernetes Troubleshooting](./topics/kubernetes-troubleshooting.md)** – Pod debugging, ImagePullBackOff, performance monitoring
- **[Terraform & IaC](./topics/terraform-iac.md)** – State management, modules, drift detection, rollback strategies
- **[Secrets & Security](./topics/secrets-security.md)** – Secret management, RBAC, encryption, security scanning
- **[Monitoring & Logging](./topics/monitoring-logging.md)** – Prometheus, ELK, centralized logging, alerting

---

### Author
**Velanati Naveen Kumar**
- DevOps Engineer  
- CI/CD | AWS | Kubernetes | Terraform | GitOps | Automation
- Connect with me: [LinkedIn](https://www.linkedin.com/in/naveenvelanati/)
- 📞 +91 9848545101

