# Advanced AWS DevOps – Production Design & Troubleshooting Scenarios
## Real Interview Questions with Architecture, Root Cause & Resolution

This document covers **real-world AWS & DevOps interview questions**, answered using:
- Architecture design
- Root cause analysis
- Troubleshooting steps
- Reliability & scalability improvements

---

## 1. How do you design a highly available architecture across Multi-AZ & Multi-Region?

### Design
- Multi-AZ ALB + Auto Scaling Group
- Stateless application layer
- RDS Multi-AZ / DynamoDB Global Tables
- S3 Cross-Region Replication
- Route53 failover or latency routing

### Why
Single AZ or region failures cause full outages.

### Troubleshooting
- Verify health checks
- Validate DNS failover
- Test regional failover regularly

### Outcome
- AZ failure → no downtime
- Region failure → minimal RTO

---

## 2. Auto Scaling didn’t scale properly — root cause?

### Root Cause
- Wrong CloudWatch metric
- CPU threshold too high
- Cooldown misconfigured
- App not CPU-bound

### Troubleshooting
1. Check ASG scaling policies
2. Review CloudWatch metrics
3. Validate instance warm-up time

### Fix
- Use target tracking
- Add custom metrics if needed

---

## 3. How do you secure cross-account access using IAM roles?

### Design
- Create IAM role in target account
- Trust relationship with source account
- Use STS AssumeRole

### Why
Avoid sharing long-term credentials.

### Troubleshooting
- Verify trust policy
- Check permission boundaries
- Use IAM policy simulator

---

## 4. 100+ microservices on ECS/EKS — deployment & rollback strategy?

### Approach
- Helm charts / GitOps (Argo CD)
- Separate namespaces
- Versioned images
- Canary or Blue-Green releases

### Rollback
- Helm rollback
- Git revert (GitOps)

### Benefit
- Independent releases
- Faster recovery

---

## 5. Production pipeline deployment failed — troubleshooting steps

### Steps
1. Check CI logs
2. Validate build artifacts
3. Verify secrets/configs
4. Inspect Kubernetes events
5. Rollback immediately

### Improvement
- Add pre-deployment validation
- Canary deployments

---

## 6. Explain your CI/CD pipeline architecture

### Architecture
- GitHub/GitLab → Jenkins / CodePipeline
- Build → Test → Scan → Deploy
- Docker → ECR → EKS
- Argo CD for CD

### Benefit
- Automated, auditable, scalable

---

## 7. Zero-downtime deployments — real example

### Implementation
- Multiple replicas
- Readiness probes
- Rolling updates
- ALB health checks

### Result
- No user impact
- Instant rollback

---

## 8. Key CloudWatch metrics for EC2, ECS, RDS

### EC2
- CPUUtilization
- Disk I/O
- NetworkIn/Out

### ECS
- CPU & memory reservation
- Task restarts

### RDS
- CPU
- FreeStorageSpace
- Read/Write latency

---

## 9. Centralized logging for microservices

### Stack
- Fluent Bit
- CloudWatch Logs / OpenSearch
- Correlation IDs

### Benefit
- Faster RCA
- Unified visibility

---

## 10. EC2 crashed — what did you do?

### Root Cause
- Disk full
- OOM
- Kernel panic

### Troubleshooting
1. Check system logs
2. Review CloudWatch alarms
3. Restore from AMI if needed

---

## 11. Secret rotation (Secrets Manager / Parameter Store)

### Approach
- Enable automatic rotation
- Lambda-based rotation
- Short TTL credentials

### Benefit
- Reduced blast radius

---

## 12. Service slow — AWS performance debugging

### Steps
- ALB latency
- EC2 CPU/memory
- DB query latency
- Network path analysis

---

## 13. AWS cost optimization (EC2, NAT, S3)

### EC2
- Right-sizing
- Spot instances

### NAT
- Minimize cross-AZ traffic
- NAT per AZ

### S3
- Lifecycle policies
- Intelligent Tiering

---

## 14. DR & Backup strategy

### Strategy
- Defined RTO & RPO
- AWS Backup
- Cross-region replication
- Periodic restore testing

---

## 15. IaC strategy (Terraform / CloudFormation)

### Approach
- Modular Terraform
- Remote state
- Environment separation
- CI validation

---

## 16. RDS Multi-AZ failover handling

### What Happens
- Automatic failover
- Endpoint switches

### Post-Failover
- Verify app reconnect logic
- Monitor latency

---

## 17. Blue-Green vs Canary (real examples)

| Blue-Green | Canary |
|---------|--------|
| Instant switch | Gradual traffic |
| Fast rollback | Safer testing |

---

## 18. API Gateway + Lambda microservices

### Design
- Stateless Lambdas
- API Gateway throttling
- IAM auth
- DLQs

---

## 19. Enterprise VPC best practices

- Hub & spoke model
- Separate accounts
- Private subnets
- Centralized logging VPC

---

## 20. Real production outage — learning

### Cause
DB connection exhaustion

### Fix
- Connection pooling
- Read replicas

### Learning
- Monitor limits early

---

## 21. Fault-tolerant design if AZ goes down

- Multi-AZ
- Stateless apps
- Health checks
- Auto scaling

---

## 22. Zero-downtime DB migration

- Backward-compatible schema
- Blue-Green DB
- Feature flags

---

## 23. API Gateway throttling handling

- Increase limits
- Client retries
- Caching

---

## 24. High ALB latency troubleshooting

- Target response time
- Slow backend
- Network latency

---

## 25. Centralized secrets for 100+ services

- AWS Secrets Manager
- IAM-based access
- Naming conventions
- Rotation policies

---

## 26. ECS/EKS node scaling automation

- Cluster Autoscaler
- ASG scaling
- Capacity reservations

---

## 27. Pods evicted in EKS — fix?

### Cause
- Memory pressure
- Disk pressure

### Fix
- Increase node size
- Tune requests/limits

---

## 28. Observability stack design

- Metrics: Prometheus / CloudWatch
- Logs: OpenSearch
- Traces: X-Ray / Jaeger

---

## 29. Distributed tracing implementation

- Trace IDs
- Instrument apps
- Visualize request flow

---

## 30. IAM access key rotation automation

- IAM + Lambda
- Secrets Manager
- Disable old keys

---

## 31. Sudden traffic spike (10K → 200K)

- Auto Scaling
- CDN caching
- Rate limiting

---

## 32. Deployment caused CPU spike — rollback

- Immediate rollback
- Analyze diff
- Tune resource limits

---

## 33. Securing S3 in multi-account setup

- Block public access
- Bucket policies
- Access via IAM roles

---

## 34. ECS service stuck in PROVISIONING

### Causes
- Insufficient capacity
- IAM permission issues

### Fix
- Check cluster capacity
- Review service events

---

## 35. Blue/Green deployments for EKS

- Two deployments
- ALB target groups
- Switch traffic gradually

---

## 🎯 FINAL INTERVIEW ADVICE

Always explain:
1. **Architecture**
2. **Failure scenario**
3. **Root cause**
4. **Fix**
5. **Prevention**

---

### Author
**Velanati Naveen Kumar**  
DevOps Engineer  
CI/CD | AWS | Kubernetes | Terraform | GitOps | Automation  
📞 +91 9848545101
