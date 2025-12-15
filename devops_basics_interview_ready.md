# DevOps & Cloud Basics – Interview Ready Notes

This file covers **commonly asked DevOps, Cloud, Linux, Git, Docker, Kubernetes, and AWS questions** with **simple explanations and real-world understanding**.

---

## 1. What is CI/CD and why is it important?

**CI/CD** stands for:
- **CI (Continuous Integration):** Automatically building and testing code
- **CD (Continuous Deployment/Delivery):** Automatically deploying code

**Why important:**
- Faster releases
- Fewer bugs
- Automation
- Consistency

---

## 2. Difference between Git fetch and Git pull?

- `git fetch`: Downloads changes but does not merge
- `git pull`: Fetch + merge

👉 Use `fetch` to review changes safely.

---

## 3. How does Docker work internally?

Docker uses:
- Linux namespaces (isolation)
- cgroups (resource limits)
- Union File System (layers)

It packages app + dependencies into an **image**, which runs as a **container**.

---

## 4. What are Pods in Kubernetes?

A **Pod** is the smallest deployable unit in Kubernetes.
- Contains one or more containers
- Shares network & storage
- Runs on a node

---

## 5. What is Infrastructure as Code (IaC)?

Managing infrastructure using code (Terraform, CloudFormation).
- Version controlled
- Repeatable
- Automated

---

## 6. How do you check running processes in Linux?

Commands:
- `ps -ef`
- `top`
- `htop`
- `systemctl status`

---

## 7. Difference between soft link and hard link?

- **Hard link:** Points to inode, works even if original file deleted
- **Soft link:** Shortcut, breaks if original deleted

---

## 8. How do you schedule a cron job?

Steps:
1. `crontab -e`
2. Add schedule:
   ```bash
   0 2 * * * /script.sh
- **Runs daily at 2 AM**
---

## 9. Explain how Load Balancer works.

A Load Balancer:

Distributes traffic

Improves availability

Prevents server overload

## 10. What is an Auto Scaling Group?

Automatically:

Adds instances during high load

Removes during low load
Ensures availability & cost efficiency.

# 11. Difference between S3 Standard and S3 IA?

- **Standard**: Frequent access

- **IA (Infrequent Access)**: Lower cost, retrieval fee

# 12. Application running slow — what will you check first?

CPU / Memory usage

Logs

Database latency

Network latency

Load balancer metrics

## 13. Deployment failed — how do you troubleshoot?

Check pipeline logs

Check application logs

Verify configs & secrets

Roll back if needed

## 14. Pod running but service not reachable — what to check?

Service selectors

Pod labels

Endpoints

Port mismatch

Network policies

## 15. Git merge vs Git rebase?

Merge: Keeps history, safe

Rebase: Linear history, rewrites commits

## 16. What is a Dockerfile?

A file with instructions to build Docker images.
Example:

FROM nginx
COPY index.html /usr/share/nginx/html

## 17. How does Docker isolate applications?

Separate namespaces

Resource limits

Independent filesystem

## 18. What is a Kubernetes Deployment?

Manages:

ReplicaSets

Rolling updates

Scaling

Used for stateless applications.

## 19. Role of Service in Kubernetes?

Provides:

Stable IP/DNS

Load balancing

Pod discovery

## 20. NodePort vs ClusterIP?

ClusterIP: Internal access

NodePort: External via node IP

## 21. How do you create a branch in Git?
git checkout -b feature-branch

## 22. What is a pull request?

A request to:

Review code

Merge changes

Improve collaboration

## 23. CI vs CD?

- **CI**: Build & test

- **CD**: Deploy

## 24. What is a pipeline in CI/CD?

A series of automated steps:

- Build
- Test
- Deploy

# 25. What is SSH and why use it?

Secure remote access using encryption.

## 26. Public key vs Private key?

- Public key → Server
- Private key → Client (secret)

## 27. VM vs Container?

VM: Heavy, full OS

Container: Lightweight, fast

## 28. What is cloud computing?

Using computing resources over the internet instead of physical hardware.

## 29. What is an EC2 instance?

A virtual server in AWS.

## 30. What is IAM?

Identity and Access Management.
Controls who can access what.

## 31. What is a VPC?

A virtual private network in cloud.

## 32. What is an S3 bucket?

Object storage for files.

## 33. How do you monitor application logs?

- Application logs
- CloudWatch
- ELK stack
- Grafana Loki

## 34. What are Prometheus and Grafana?

- **Prometheus**: Metrics collection
- **Grafana**: Visualization

## 35. What is a YAML file?

Human-readable configuration format.
Used in:
- Kubernetes
- CI/CD pipelines

## 36. What are environment variables?

Dynamic values passed to apps at runtime.

## 37. What is a build artifact?

Output of build process:
- JAR
- WAR
- Docker image

## 38. How do you roll back a deployment?

Helm rollback
Re-deploy previous version
Git revert

## 39. What is a Helm chart?

Package manager for Kubernetes.
Contains templates + values.

## 40. Blue-Green deployment (simple)?

- **Two environments:**
- Blue = live
- Green = new
Switch traffic after testing.

## 41. What is a reverse proxy?

Forwards client requests to backend servers.
Example: Nginx

## 42. What is a Load Balancer and why needed?

Distributes traffic and ensures high availability.

## 43. How do you test an API using curl?
curl -X GET https://api.example.com

## 44. What is a container registry?

Stores container images.
Examples:
- Docker Hub
- AWS ECR

## 45. IaaS vs PaaS vs SaaS?

- IaaS: EC2
- PaaS: Elastic Beanstalk
- SaaS: Gmail


---

### Author
**Velanati Naveen Kumar**
- DevOps Engineer  
- CI/CD | AWS | Kubernetes | Terraform | GitOps | Automation
- Connect with me: [LinkedIn](https://www.linkedin.com/in/naveenvelanati/)
- 📞 +91 9848545101
