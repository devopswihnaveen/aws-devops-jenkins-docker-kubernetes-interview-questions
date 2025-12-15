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


Runs daily at 2 AM
---

