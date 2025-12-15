# Expected DevOps Interview Questions & Answers  
## Based on AWS, Jenkins, Terraform, CI/CD, Kubernetes & GitOps Skillset

This document contains **commonly expected interview questions with clear, real-world answers**, aligned with the required DevOps skillset.

---

## 1. Explain your experience with CI/CD pipelines.

I have designed and maintained CI/CD pipelines using **Jenkins/GitHub/GitLab**.  
The pipeline typically includes:
- Code checkout from Git
- Build and unit testing
- Static code analysis
- Docker image build
- Image push to registry
- Deployment to Kubernetes using Helm or GitOps

This ensures **automated, repeatable, and fast deployments**.

---

## 2. How does Jenkins fit into a CI/CD process?

Jenkins acts as the **automation engine**:
- Triggers builds via webhooks
- Executes pipelines written in Jenkinsfile
- Integrates with Git, Docker, Terraform, Kubernetes
- Handles build, test, and deployment stages

---

## 3. What is a Jenkinsfile and why is it important?

A Jenkinsfile is a pipeline definition written as code.
- Stored in Git
- Version controlled
- Reproducible
- Supports Declarative and Scripted pipelines

This follows **Pipeline as Code best practice**.

---

## 4. How do you manage source code using Git?

I use **GitHub/GitLab flow**:
- Feature branches
- Pull requests / Merge requests
- Code reviews
- Protected main branches

This ensures **collaboration, code quality, and controlled releases**.

---

## 5. Difference between Git merge and Git rebase?

- **Merge**: Preserves history, creates merge commit
- **Rebase**: Creates linear history, rewrites commits

I prefer **merge for shared branches** and **rebase for local cleanup**.

---

## 6. How do you write and use Bash/Shell scripts in DevOps?

I use shell scripts to:
- Automate builds
- Deploy applications
- Manage system tasks
- Parse logs
- Trigger Terraform/Helm commands

Shell scripting helps in **gluing tools together**.

---

## 7. What is Docker and how have you used it?

Docker packages applications with dependencies into **containers**.
I use Docker to:
- Build images
- Run containers locally
- Push images to registries
- Deploy containerized apps to Kubernetes

---

## 8. How do you reduce Docker image size?

- Multi-stage builds
- Minimal base images (alpine/distroless)
- Remove unused packages
- Use `.dockerignore`

Smaller images mean **faster deployments and better security**.

---

## 9. What is Kubernetes and why is it used?

Kubernetes is a container orchestration platform that:
- Manages container lifecycle
- Handles scaling and self-healing
- Provides service discovery
- Enables rolling updates

It is used for **reliable, scalable container deployments**.

---

## 10. What Kubernetes clusters have you worked with?

I have worked with:
- Managed Kubernetes services (AKS)
- Kubernetes clusters via Rancher
- Deploying apps using Helm and GitOps tools

---

## 11. Explain how a Kubernetes Deployment works.

A Deployment:
- Manages ReplicaSets
- Ensures desired pod count
- Supports rolling updates and rollbacks

Used for **stateless applications**.

---

## 12. How do you expose applications in Kubernetes?

Using:
- ClusterIP (internal)
- NodePort (node-level)
- LoadBalancer (cloud-managed)
- Ingress (HTTP routing)

Ingress + LoadBalancer is preferred for production.

---

## 13. What is Helm and why do you use it?

Helm is a **package manager for Kubernetes**.
- Templated manifests
- Environment-specific values
- Easy rollback
- Versioning

It simplifies Kubernetes deployments.

---

## 14. What is GitOps and how does it work?

GitOps uses **Git as the single source of truth**.
- Desired state stored in Git
- Tools like Argo CD/Flux continuously sync cluster state
- Any drift is auto-corrected

This improves **auditability and reliability**.

---

## 15. What GitOps tools have you used?

I have experience with:
- Argo CD
- Flux (basic understanding)
- Fleet (via Rancher environments)

---

## 16. How does Argo CD work?

- Watches Git repositories
- Compares desired vs live state
- Automatically syncs Kubernetes resources
- Supports rollback via Git revert

---

## 17. What is Infrastructure as Code (IaC)?

IaC means managing infrastructure using code.
Benefits:
- Version control
- Repeatability
- Automation
- Reduced manual errors

Tools used: **Terraform, Ansible**.

---

## 18. Explain how Terraform works.

Terraform workflow:
1. `terraform init`
2. `terraform plan`
3. `terraform apply`

Terraform uses a **state file** to track infrastructure.

---

## 19. How do you manage Terraform state in a team?

- Remote backend (S3/Azure Storage)
- State locking (DynamoDB / Blob locks)
- Restricted access
- Separate state per environment

---

## 20. How do you manage secrets in Terraform and CI/CD?

- Environment variables
- Secret managers (AWS SSM, Azure Key Vault)
- CI secret stores
- Never hardcode secrets

---

## 21. What is Ansible and when do you use it?

Ansible is used for:
- Configuration management
- Server provisioning
- Application setup

I use Terraform for infra and Ansible for **configuration**.

---

## 22. How do you handle zero-downtime deployments?

- Multiple replicas
- Readiness probes
- Rolling updates / Canary
- Load balancers
- Helm rollback if needed

---

## 23. How do you troubleshoot a failed deployment?

Steps:
- Check CI/CD logs
- Check application logs
- Verify configs and secrets
- Check Kubernetes events
- Rollback if required

---

## 24. How do you monitor applications?

- Logs (ELK, Cloud logs)
- Metrics (Prometheus)
- Dashboards (Grafana)
- Alerts

---

## 25. How do you handle learning new tools quickly?

- Official documentation
- Hands-on labs
- Proof-of-concept projects
- Internal knowledge sharing

Adaptability is key in DevOps.

---

## 26. Do you have experience with Azure?

Yes, I have experience with:
- Azure DevOps / AKS (basic to intermediate)
- Azure storage and networking concepts

Azure experience complements AWS skills.

---

## 27. Why should we hire you as a DevOps Engineer?

- Strong CI/CD and automation mindset
- Hands-on AWS, Kubernetes, Terraform experience
- GitOps knowledge
- Problem-solving attitude
- Continuous learner

---

## 📌 Final Interview Tip

Always explain:
- **What you did**
- **Why you chose that approach**
- **What problem it solved**
- **How you improved reliability or speed**

---

### Author
Velanati Naveen Kumar
DevOps Engineer  
CI/CD | AWS | Kubernetes | Terraform | GitOps | Automation
Connect with me: [LinkedIn](https://www.linkedin.com/in/naveenvelanati/)
