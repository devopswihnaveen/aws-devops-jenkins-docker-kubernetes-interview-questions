# Kubernetes Objects – Detailed Explanation (Interview & Production Ready)

This document explains **core Kubernetes objects**, their **purpose**, **how they work**, **real-world use cases**, and **common troubleshooting points**.  
Ideal for **DevOps / Platform Engineer interviews and hands-on learning**.

---

## 1. What are Kubernetes Objects?

Kubernetes objects are **persistent entities** that represent the **desired state** of your cluster.

They define:
- What applications should run
- How many replicas
- How they are exposed
- How they are configured and secured

Kubernetes continuously works to **match the current state with the desired state** defined by these objects.

---

## 2. Pod

### What is a Pod?
A **Pod** is the **smallest deployable unit** in Kubernetes.

It can contain:
- One container (most common)
- Multiple tightly coupled containers (sidecar pattern)

### Key Characteristics
- Shared network (same IP)
- Shared storage (volumes)
- Ephemeral (not long-lived)

### Real Use Case
- Running a single microservice
- App container + logging sidecar

### Troubleshooting
- Pod restarts → Check logs
- Pod Pending → Check resources / scheduling

---

## 3. ReplicaSet

### What is a ReplicaSet?
Ensures a **specified number of pod replicas** are running at all times.

### Why It’s Used
- Handles pod failures
- Maintains availability

⚠️ Usually **not created directly** — managed by Deployments.

---

## 4. Deployment

### What is a Deployment?
A Deployment manages:
- ReplicaSets
- Pod scaling
- Rolling updates
- Rollbacks

### Real Use Case
- Stateless applications (web apps, APIs)

### Key Features
- Rolling updates
- Zero-downtime deployments
- Easy rollback

### Troubleshooting
- Pods not updating → Check rollout status
- Slow rollout → Review readiness probes

---

## 5. StatefulSet

### What is a StatefulSet?
Used for **stateful applications** that require:
- Stable pod identity
- Persistent storage
- Ordered startup/shutdown

### Real Use Case
- Databases (MySQL, MongoDB)
- Kafka, Elasticsearch

### Difference from Deployment
- Pods have fixed names
- Persistent volumes per pod

---

## 6. DaemonSet

### What is a DaemonSet?
Ensures **one pod runs on every node** (or selected nodes).

### Real Use Case
- Log collectors (Fluentd, Fluent Bit)
- Monitoring agents
- Security agents

---

## 7. Service

### What is a Service?
Provides a **stable network endpoint** to access pods.

### Types of Services
| Type | Use |
|----|----|
| ClusterIP | Internal access |
| NodePort | Access via node IP |
| LoadBalancer | External cloud LB |

### Real Use Case
- Exposing backend services
- Load balancing traffic to pods

---

## 8. Ingress

### What is an Ingress?
Manages **HTTP/HTTPS routing** to services.

### Why Use Ingress?
- Path-based routing
- Host-based routing
- SSL termination

### Example
```text
/api → backend-service
/web → frontend-service

```

## 9. ConfigMap

### What is a ConfigMap?
A **ConfigMap** is used to store **non-sensitive configuration data** separately from application code.

### What it Stores
- Application properties
- Environment variables
- Configuration files

### Why It’s Used
- Avoid rebuilding Docker images for config changes
- Environment-specific configuration (dev/stage/prod)

### Real-World Example
- Database host
- Feature flags
- Application ports

### Troubleshooting
- App not picking config → Check mount/env mapping
- Config updated but app unchanged → Restart pods

---

## 10. Secret

### What is a Secret?
A **Secret** stores **sensitive information** such as:
- Passwords
- Tokens
- API keys
- Certificates

### How It’s Stored
- Base64 encoded
- Encrypted at rest (if enabled)

### Best Practices
- Restrict access using RBAC
- Avoid committing secrets to Git
- Use external secret managers (AWS Secrets Manager)

### Troubleshooting
- Pod fails to start → Check secret name/key
- Access denied → Verify RBAC permissions

---

## 11. Namespace

### What is a Namespace?
A **Namespace** provides **logical isolation** within a Kubernetes cluster.

### Use Cases
- Environment separation (dev/prod)
- Team isolation
- Resource quota enforcement

### Benefits
- Prevents naming conflicts
- Improves security and manageability

---

## 12. Volume

### What is a Volume?
A **Volume** provides storage to a pod and is mounted inside containers.

### Key Point
- Lifecycle tied to pod
- Data lost when pod is deleted (for most volume types)

### Use Case
- Temporary cache
- Shared data between containers in a pod

---

## 13. PersistentVolume (PV)

### What is a PersistentVolume?
A **PersistentVolume** is a **cluster-wide storage resource**.

### Characteristics
- Independent of pod lifecycle
- Backed by storage (EBS, EFS, NFS)

### Use Case
- Databases
- Persistent application data

---

## 14. PersistentVolumeClaim (PVC)

### What is a PVC?
A **PVC** is a request for storage by a pod.

### How It Works
- Pod requests storage via PVC
- PVC binds to a matching PV

### Troubleshooting
- PVC stuck in Pending → No matching PV or StorageClass
- Mount error → Check permissions & volume type

---

## 15. Job

### What is a Job?
A **Job** runs a **task to completion**.

### Use Cases
- Database migration
- Batch processing
- One-time scripts

### Troubleshooting
- Job failing → Check pod logs
- Job reruns → Check restart policy

---

## 16. CronJob

### What is a CronJob?
A **CronJob** runs Jobs on a **schedule**, similar to Linux cron.

### Use Cases
- Backups
- Cleanup jobs
- Report generation

### Troubleshooting
- Job not running → Check schedule format
- Too many jobs → Configure job history limits

---

## 17. Horizontal Pod Autoscaler (HPA)

### What is HPA?
HPA automatically scales pods based on:
- CPU usage
- Memory usage
- Custom metrics

### Requirements
- Metrics Server must be installed

### Troubleshooting
- HPA not scaling → Metrics server missing
- Scaling delayed → Incorrect resource requests

---

## 18. Node

### What is a Node?
A **Node** is a worker machine where pods run.

### Types
- Virtual machines (EC2)
- Bare-metal servers

### Troubleshooting
- Node NotReady → Check kubelet, disk, network
- Pods not scheduled → Resource exhaustion

---

## 19. ServiceAccount

### What is a ServiceAccount?
A **ServiceAccount** provides an identity to pods.

### Use Cases
- Access Kubernetes API
- Access cloud services (IRSA in AWS)

### Best Practice
- One service account per application

---

## 20. Role & RoleBinding

### Role
Defines **permissions within a namespace**.

### RoleBinding
Binds Role to:
- User
- Group
- ServiceAccount

### Use Case
- Restrict developer access to dev namespace

---

## 21. ClusterRole & ClusterRoleBinding

### What Are They?
- Define **cluster-wide permissions**
- Used by controllers and admins

### Example Use Case
- Monitoring tools
- Ingress controllers

---

## 22. NetworkPolicy

### What is a NetworkPolicy?
Controls **network traffic between pods**.

### Why It’s Needed
- Zero-trust security
- Prevent lateral movement

### Troubleshooting
- Traffic blocked → Check policy rules
- Policy not working → CNI plugin support

---

## 23. ResourceQuota

### What is ResourceQuota?
Limits **total resource usage** in a namespace.

### Why Use It?
- Prevent resource starvation
- Fair usage across teams

---

## 24. LimitRange

### What is LimitRange?
Defines default **resource requests and limits** for pods.

### Benefit
- Prevents pods without limits
- Improves cluster stability

---

## 25. Lifecycle Hooks

### What are Lifecycle Hooks?
Hooks executed during:
- `postStart` – after container starts
- `preStop` – before container stops

### Use Case
- Graceful shutdown
- Cleanup operations

---

## 26. Final Interview Summary

> “From ConfigMaps to lifecycle hooks, Kubernetes objects help manage configuration, security, storage, scaling, and access control. Together, they enable scalable, secure, and resilient containerized applications.”

---

### Author
**Velanati Naveen Kumar**  
DevOps Engineer  
CI/CD | AWS | Kubernetes | Terraform | GitOps | Automation  
📞 +91 9848545101
