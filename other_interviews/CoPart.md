# DevOps, Kubernetes, Linux, Azure, Terraform & Git – Interview Questions and Answers

---

## ⚙️ DevOps & CI/CD

### 1. What are your day-to-day activities as a DevOps Engineer?

**Answer:**
- Managing CI/CD pipelines (build, test, deploy)
- Automating infrastructure using IaC tools
- Monitoring application and infrastructure health
- Troubleshooting production issues
- Managing cloud resources and costs
- Collaborating with developers and security teams
- Improving reliability, scalability, and performance

---

### 2. How do you ensure stability and efficiency in CI/CD and cloud environments?

**Answer:**
- Implement automated testing and validation
- Use version-controlled pipeline configurations
- Enable monitoring and alerting
- Apply least-privilege security policies
- Use auto-scaling and load balancing
- Regularly review logs and metrics

---

### 3. Explain your CI/CD pipeline flow.

**Answer:**
- Code commit to Git repository
- Automated build triggered
- Unit and security tests executed
- Container image built and scanned
- Image pushed to registry
- Deployment to staging
- Manual/automated approval
- Production deployment
- Post-deployment monitoring

---

### 4. What happens during Continuous Delivery (CD)?

**Answer:**
- Validated code is automatically prepared for release
- Artifacts are packaged and versioned
- Deployments are automated up to production
- Release is controlled via approvals or triggers
- Ensures rapid and reliable releases

---

### 5. How do you manage pipeline configurations and rollback strategies?

**Answer:**
- Store pipelines as code in Git
- Use versioned artifacts and tags
- Enable rollback via previous deployments
- Maintain deployment history
- Test rollback procedures regularly

---

## ☸️ Kubernetes / AKS

### 6. How do you troubleshoot a CrashLoopBackOff? What are the common causes?

**Answer:**
**Common Causes:**
- Application crash
- Wrong command or entrypoint
- Missing secrets or configs
- Resource limits exceeded
- Aggressive probes

**Troubleshooting:**
- Check pod logs and events
- Describe pod
- Validate configs and secrets
- Adjust probes or resources

---

### 7. If a pod is down, how do you debug it step-by-step?

**Answer:**
- Check pod status
- Review logs
- Describe pod for events
- Check node status
- Verify resource limits
- Validate networking and storage

---

### 8. If a pod loses network connectivity, how do you identify and fix it?

**Answer:**
- Test connectivity inside the pod
- Check service and endpoint configuration
- Verify DNS resolution
- Inspect network policies
- Check CNI plugin health
- Fix misconfigurations or policies

---

### 9. Why are StatefulSets useful? How are they different from Deployments?

**Answer:**
- StatefulSets maintain stable identity and storage
- Used for databases and stateful apps
- Deployments are for stateless applications
- StatefulSets support ordered scaling and updates

---

### 10. Difference between Persistent Volume (PV) and Persistent Volume Claim (PVC).

**Answer:**
- **PV:** Actual storage resource in the cluster
- **PVC:** Request for storage by a pod
- PVC binds to a suitable PV based on requirements

---

### 11. How do you manage Kubernetes YAML manifests across environments?

**Answer:**
- Use Helm or Kustomize
- Maintain environment-specific values
- Store manifests in Git
- Use CI/CD for validation and deployment

---

### 12. How do you secure a public AKS/Kubernetes cluster?

**Answer:**
- Enable RBAC and least privilege
- Use private endpoints where possible
- Implement network policies
- Secure secrets properly
- Enable logging and monitoring
- Regular security scans

---

### 13. Where and how do you store cluster information securely?

**Answer:**
- Use secret managers or encrypted storage
- Restrict access using RBAC
- Store kubeconfig securely
- Enable audit logging

---

## 🐧 Linux & System Troubleshooting

### 14. Difference between Hard link vs Soft link.

**Answer:**
- **Hard link:** Points to inode, survives file deletion
- **Soft link:** Points to file path, breaks if file is removed

---

### 15. A user can’t access a file — how do you grant permissions?

**Answer:**
- Check file ownership and permissions
- Use `chmod` to modify permissions
- Use `chown` to change ownership
- Verify group membership

---

### 16. A process is consuming high CPU or memory — how do you monitor and handle it?

**Answer:**
- Use `top`, `htop`, or `ps`
- Identify PID
- Analyze logs
- Restart or optimize process
- Scale resources if needed

---

### 17. A user can’t SSH into a server — how do you troubleshoot?

**Answer:**
- Check SSH service status
- Verify credentials and permissions
- Check firewall and security groups
- Review SSH logs
- Validate network connectivity

---

## ☁️ Azure & Cloud

### 18. What is a VNet and NSG in Azure?

**Answer:**
- **VNet:** Private network in Azure
- **NSG:** Controls inbound and outbound traffic rules

---

### 19. What is Azure AD (Microsoft Entra ID) and why is it used?

**Answer:**
- Identity and access management service
- Used for authentication and authorization
- Enables SSO and role-based access

---

### 20. How do you reduce and manage cloud costs effectively?

**Answer:**
- Monitor resource usage
- Use auto-scaling
- Delete unused resources
- Choose right pricing models
- Set budgets and alerts

---

## 🏗️ Terraform & Git

### 21. Explain the Terraform lifecycle.

**Answer:**
- `init` – Initialize configuration
- `plan` – Preview changes
- `apply` – Create/update resources
- `destroy` – Remove resources

---

### 22. How do you handle Terraform state management?

**Answer:**
- Use remote backend
- Enable state locking
- Restrict access
- Backup state files

---

### 23. Difference between git fetch and git pull.

**Answer:**
- `git fetch` downloads changes without merging
- `git pull` fetches and merges changes

---

### 24. How do you handle merge conflicts in Git?

**Answer:**
- Identify conflicting files
- Manually resolve conflicts
- Test changes
- Commit resolved files

---

✅ **This `.md` file is interview-ready and ideal for your DevOps portfolio website.**

If you want, I can:
- Convert this into **HTML pages**
- Merge with your Kubernetes troubleshooting docs
- Create **PDF / PPT versions**
- Add **real-world examples**

Just tell me 👍
