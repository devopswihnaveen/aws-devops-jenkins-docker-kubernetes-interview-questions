# Cause & Troubleshooting – AWS | Docker | Kubernetes | Terraform
## Real-World Failure Scenarios + Resolution Steps (Interview Ready)

This document explains **common cloud & DevOps issues**, their **root causes**, and **step-by-step troubleshooting approaches** used in production environments.

---

# ☁️ AWS – CAUSE & TROUBLESHOOTING

## 1. Security Groups vs NACLs – Traffic Not Working

### Cause
- SG missing inbound rule
- NACL explicitly denying traffic

### Troubleshooting
1. Check Security Group inbound/outbound rules
2. Verify NACL allow rules (both directions)
3. Confirm correct subnet association

### Interview Point
> SG is stateful, NACL is stateless — explicit deny in NACL blocks traffic.

---

## 2. Application Downtime – Single AZ Architecture

### Cause
- Resources deployed in only one AZ

### Troubleshooting
1. Verify subnet AZ distribution
2. Enable Multi-AZ for ALB, ASG, RDS
3. Add health checks & failover

---

## 3. Storage Issues – S3 vs EBS vs EFS Misuse

### Cause
- Using EBS for shared storage
- Using S3 for low-latency workloads

### Troubleshooting
- Shared access → Use EFS
- OS/DB storage → Use EBS
- Backup/static content → Use S3

---

## 4. High Traffic But App Still Slow

### Cause
- Load balancer exists but no Auto Scaling

### Troubleshooting
1. Enable Auto Scaling Group
2. Define scaling policies
3. Monitor CPU & latency metrics

---

## 5. IAM Access Denied Errors

### Cause
- Role not attached
- Explicit deny in policy

### Troubleshooting
1. Review IAM policy simulator
2. Check trust relationship
3. Look for explicit deny

---

## 6. Unexpected EC2 Termination

### Cause
- Spot instance interruption
- Auto Scaling scale-in

### Troubleshooting
1. Check instance lifecycle
2. Review ASG activity
3. Enable termination protection (if needed)

---

## 7. S3 Data Exposed Publicly

### Cause
- Public bucket policy
- Public ACL

### Troubleshooting
1. Enable Block Public Access
2. Remove public bucket policy
3. Audit via AWS Config

---

## 8. Disaster Recovery Failure

### Cause
- RTO/RPO not defined
- No replication or backups

### Troubleshooting
1. Define RTO & RPO
2. Enable cross-region replication
3. Test DR regularly

---

# 🐳 DOCKER – CAUSE & TROUBLESHOOTING

## 9. Container Exits Immediately

### Cause
- Main process crashed
- CMD/ENTRYPOINT misconfigured

### Troubleshooting
1. Check `docker logs`
2. Verify CMD/ENTRYPOINT
3. Run container interactively

---

## 10. Large Docker Image Size

### Cause
- Using full OS image
- Build tools inside runtime image

### Troubleshooting
1. Use multi-stage builds
2. Switch to alpine/distroless
3. Clean package cache

---

## 11. Data Loss After Container Restart

### Cause
- No persistent volume used

### Troubleshooting
1. Use Docker volumes
2. Use bind mounts
3. Externalize data storage

---

## 12. Docker Build Very Slow

### Cause
- Poor Dockerfile layer ordering

### Troubleshooting
1. Move rarely-changing steps up
2. Leverage layer caching
3. Reduce COPY scope

---

## 13. Container Vulnerabilities Found

### Cause
- Outdated base image
- Unpatched dependencies

### Troubleshooting
1. Scan images (Trivy/Snyk)
2. Update base image
3. Remove unused packages

---

# ☸️ KUBERNETES – CAUSE & TROUBLESHOOTING

## 14. Pod Running but Service Unreachable

### Cause
- Service selector mismatch
- Wrong port mapping

### Troubleshooting
1. Check labels vs selectors
2. Verify endpoints
3. Validate container port

---

## 15. Pod Restarting Frequently (CrashLoopBackOff)

### Cause
- App crash
- Resource limits too low

### Troubleshooting
1. Check pod logs
2. Increase CPU/memory
3. Fix application error

---

## 16. High Node CPU / Memory Pressure

### Cause
- Too many pods per node
- No resource limits

### Troubleshooting
1. Describe node
2. Enable Cluster Autoscaler
3. Tune resource requests

---

## 17. Application Gets Traffic Before Ready

### Cause
- Missing readiness probe

### Troubleshooting
1. Add readiness probe
2. Validate startup time
3. Use proper health endpoints

---

## 18. HPA Not Scaling Pods

### Cause
- Metrics server missing
- Incorrect resource requests

### Troubleshooting
1. Verify metrics server
2. Check HPA config
3. Review CPU requests

---

## 19. Secret Exposure Risk

### Cause
- Secrets stored in plain YAML
- Excess RBAC permissions

### Troubleshooting
1. Encrypt secrets at rest
2. Use external secret managers
3. Restrict RBAC access

---

## 20. Pods Scheduled on Wrong Nodes

### Cause
- Missing affinity/taints

### Troubleshooting
1. Define node affinity
2. Use taints & tolerations
3. Verify scheduling events

---

# 🌍 TERRAFORM – CAUSE & TROUBLESHOOTING

## 21. Terraform Apply Failed Midway

### Cause
- API limit
- Invalid configuration

### Troubleshooting
1. Fix error
2. Re-run `terraform apply`
3. Manually clean partial resources if needed

---

## 22. Terraform State Corruption

### Cause
- Local state usage
- Concurrent applies

### Troubleshooting
1. Use remote backend (S3)
2. Enable state locking (DynamoDB)
3. Restrict access

---

## 23. Configuration Drift Detected

### Cause
- Manual changes via console

### Troubleshooting
1. Run `terraform plan`
2. Re-apply desired state
3. Enforce IaC-only changes

---

## 24. Duplicate Resource Creation

### Cause
- Incorrect count usage

### Troubleshooting
1. Replace count with for_each
2. Import existing resources
3. Review state file

---

## 25. Environment Mix-Up (Prod resources in Dev)

### Cause
- Shared state files
- Same backend config

### Troubleshooting
1. Separate state per environment
2. Use workspaces or directories
3. Enforce access controls

---

# 📌 INTERVIEW GOLDEN RULE

When explaining troubleshooting:
1. **Identify symptoms**
2. **Find root cause**
3. **Fix immediately**
4. **Add prevention measures**

---

### Author
Cloud / DevOps Engineer  
Production Troubleshooting | AWS | Docker | Kubernetes | Terraform
