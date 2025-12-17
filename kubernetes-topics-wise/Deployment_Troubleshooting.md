# Deployment Troubleshooting – Interview Questions & Answers

## Question 1  
### During a deployment, the application fails to start, and the logs show errors related to container image pulling.  
**How would you troubleshoot and resolve this deployment failure?**

**Answer:**
- Check pod events using `kubectl describe pod`
- Verify image name, tag, and registry URL
- Confirm image exists in the registry
- Validate imagePullSecrets and registry credentials
- Check node network access and DNS
- Try pulling the image manually from a node
- Fix image reference or permissions and redeploy

---

## Question 2  
### After a deployment, users report intermittent 500 errors when accessing the application.  
**What steps would you take to identify the root cause of these errors and rectify the deployment failure?**

**Answer:**
- Review application logs for exceptions
- Check readiness and liveness probes
- Inspect ingress / load balancer logs
- Monitor CPU and memory usage
- Verify database and external service connectivity
- Tune probes, fix code issues, or increase resources

---

## Question 3  
### The deployment completes successfully, but the application behaves differently in the production environment compared to the testing environment.  
**How would you investigate and address this deployment failure?**

**Answer:**
- Compare environment variables, ConfigMaps, and Secrets
- Check dependency and runtime versions
- Validate feature flags
- Compare production and test data
- Review infra differences (network, security, storage)
- Standardize configs and improve environment parity

---

## Question 4  
### After a deployment, the application experiences a significant increase in response time.  
**How would you troubleshoot and mitigate this deployment failure?**

**Answer:**
- Analyze metrics using monitoring tools
- Check autoscaling configuration (HPA)
- Review application and database logs
- Inspect load balancer routing and health checks
- Optimize code or database queries
- Scale resources if required

---

## Question 5  
### A deployment fails due to resource constraints in the Kubernetes cluster.  
**What steps would you take to resolve this deployment failure and prevent future occurrences?**

**Answer:**
- Review pod events for insufficient resources
- Check node capacity and utilization
- Adjust resource requests and limits
- Scale nodes or enable cluster autoscaler
- Implement HPA and resource quotas
- Perform capacity planning

---

## Question 6  
### The deployment process hangs at a particular stage, without any error messages.  
**How would you troubleshoot this deployment failure and resume the deployment process?**

**Answer:**
- Check rollout status of the deployment
- Inspect pending or stuck pods
- Review events and scheduler messages
- Analyze CI/CD pipeline logs
- Identify Helm hooks or blocking jobs
- Fix root cause and restart or rollback deployment

---

## Question 7  
### After a deployment, some users report missing or corrupted data in the application.  
**How would you investigate and rectify this deployment failure?**

**Answer:**
- Verify database migration scripts
- Check recent backups
- Review application and database logs
- Compare data before and after deployment
- Restore from backup if needed
- Improve migration testing and rollback strategies

---

## Question 8  
### The deployment succeeds, but the application experiences frequent crashes or restarts.  
**What steps would you take to diagnose and resolve this deployment failure?**

**Answer:**
- Check pod status for CrashLoopBackOff
- Inspect container logs
- Review liveness and readiness probes
- Check for OOMKilled or resource limit issues
- Adjust probes or increase resources
- Fix application-level bugs

---

## Question 9  
### After a deployment, the application's UI appears broken or distorted.  
**How would you troubleshoot and fix this deployment failure?**

**Answer:**
- Verify correct frontend build is deployed
- Clear browser and CDN cache
- Check static asset paths and base URLs
- Inspect browser console for errors
- Rebuild and redeploy frontend assets

---

## Question 10  
### The deployment process fails due to conflicts or inconsistencies in the Helm charts.  
**How would you address this deployment failure and ensure Helm chart consistency?**

**Answer:**
- Run `helm lint` to validate charts
- Review environment-specific values files
- Render templates using `helm template`
- Resolve chart and dependency version mismatches
- Follow semantic versioning
- Enforce Helm validation in CI/CD pipelines

---

## Question 11  
### A deployment fails due to insufficient permissions or access rights.  
**How would you troubleshoot and rectify this deployment failure related to permissions?**

**Answer:**
- Check error messages for `AccessDenied`, `Forbidden`, or `Unauthorized`
- Verify Kubernetes RBAC (Role, ClusterRole, RoleBinding)
- Ensure correct ServiceAccount is attached to the pod
- Check cloud IAM roles and policies (AWS IAM / Azure RBAC)
- Validate permissions for resources like secrets, configmaps, volumes
- Fix missing permissions and re-deploy
- Follow least-privilege principle to prevent future issues

---

## Question 12  
### The deployment process shows errors related to secrets or sensitive configuration data.  
**How would you handle this deployment failure and ensure secure handling of secrets?**

**Answer:**
- Check if Kubernetes Secrets exist and are correctly referenced
- Validate secret keys and environment variable mappings
- Ensure secrets are base64-encoded correctly
- Confirm RBAC permissions allow access to secrets
- Avoid hardcoding secrets in YAML or pipelines
- Use secret managers (AWS Secrets Manager, HashiCorp Vault)
- Rotate compromised secrets and redeploy securely

---

## Question 13  
### The deployment fails due to network connectivity issues between application components.  
**How would you diagnose and resolve this deployment failure related to network connectivity?**

**Answer:**
- Verify service names and ports
- Check Kubernetes Services and Endpoints
- Inspect NetworkPolicies blocking traffic
- Validate DNS resolution between pods
- Test connectivity using `curl`, `ping`, or `nslookup` from pods
- Check security groups / firewall rules
- Fix networking rules and redeploy

---

## Question 14  
### The deployment process fails due to insufficient disk space or storage capacity.  
**How would you address this deployment failure caused by disk space constraints?**

**Answer:**
- Check node disk usage
- Inspect pod events for `DiskPressure`
- Validate PVC and storage class configuration
- Increase disk size or attach larger volumes
- Clean up unused images and logs
- Set proper storage requests and limits
- Monitor disk usage proactively

---

## Question 15  
### The deployment fails due to compatibility issues between application components and external dependencies.  
**How would you handle this deployment failure caused by compatibility issues?**

**Answer:**
- Identify failing dependency from logs
- Verify version compatibility of libraries and APIs
- Check runtime versions (Java, Node, Python)
- Use dependency locking (package-lock, requirements.txt)
- Test compatibility in staging
- Roll back to a stable version if needed
- Document supported dependency versions

---

## Question 16  
### The deployment process encounters errors related to DNS resolution or domain name configuration.  
**How would you troubleshoot and resolve this deployment failure associated with DNS issues?**

**Answer:**
- Check CoreDNS pod health
- Validate service and ingress DNS names
- Test DNS resolution using `nslookup` or `dig`
- Verify external DNS records (Route53, Cloud DNS)
- Check ingress controller configuration
- Fix DNS entries and restart affected pods

---

## Question 17  
### The deployment fails due to conflicts or inconsistencies in the environment variables or configuration settings.  
**How would you address this deployment failure related to configuration inconsistencies?**

**Answer:**
- Compare environment variables across environments
- Review ConfigMaps and Secrets
- Validate application config files
- Check Helm values files for overrides
- Remove duplicate or conflicting variables
- Standardize configuration management
- Use schema validation for configs

---

## Question 18  
### The deployment process fails due to timeouts or connectivity issues with external services or APIs.  
**How would you troubleshoot and rectify this deployment failure related to external dependencies?**

**Answer:**
- Check application logs for timeout errors
- Test connectivity to external services from pods
- Validate network routes and firewall rules
- Check API rate limits and quotas
- Configure retries and timeouts properly
- Use circuit breakers and fallback mechanisms
- Monitor dependency health

---

## Question 19  
### The deployment fails due to a misconfigured or invalid SSL certificate for HTTPS communication.  
**How would you handle this deployment failure associated with SSL certificate issues?**

**Answer:**
- Inspect certificate validity and expiry
- Verify certificate chain and trust store
- Check ingress or load balancer TLS configuration
- Ensure correct domain-to-certificate mapping
- Renew or replace expired certificates
- Use automated certificate management (cert-manager)
- Test HTTPS endpoints after fix

---

## Question 20  
### After deploying a microservices app, auth-service and user-profile-service both crash due to unexpected port conflicts.  
**How would you troubleshoot and resolve this issue?**

**Answer:**
- Check container logs for port binding errors
- Verify containerPort and service port configurations
- Ensure unique ports for each service
- Check hostPort usage (avoid unless necessary)
- Review Helm values or deployment YAML
- Update port configurations and redeploy
- Standardize port allocation across microservices

---

# Kubernetes Deployment Failure Scenarios With Erroe Messages/Code

## Scenario 1: CrashLoopBackOff  
**What it means:**  
The container starts but crashes repeatedly, and Kubernetes keeps restarting it.

**How to troubleshoot & fix:**
- Check container logs using `kubectl logs <pod>`
- Describe the pod to review events
- Verify application startup command and arguments
- Check environment variables and config files
- Inspect liveness/readiness probes (may be too aggressive)
- Check resource limits (memory/CPU)
- Fix application error or configuration and redeploy

---

## Scenario 2: ImagePullBackOff  
**What it means:**  
Kubernetes cannot pull the container image.

**How to troubleshoot & fix:**
- Verify image name and tag
- Ensure image exists in registry
- Check imagePullSecrets
- Validate registry credentials
- Ensure nodes have internet access
- Fix permissions or image reference and redeploy

---

## Scenario 3: No Pod Created  
**What it means:**  
Deployment exists, but no pods are created.

**How to troubleshoot & fix:**
- Check deployment status
- Verify replica count is greater than zero
- Check namespace correctness
- Inspect events for validation errors
- Ensure no admission controller or policy is blocking pods
- Fix deployment spec and reapply

---

## Scenario 4: kubectl apply fails  
**What it means:**  
Manifest fails validation or API server rejects it.

**How to troubleshoot & fix:**
- Check YAML syntax and indentation
- Validate API version and kind
- Run `kubectl apply --dry-run=client`
- Ensure referenced resources exist (namespace, configmap, secret)
- Fix errors and reapply the manifest

---

## Scenario 5: Pod stuck in Pending state  
**What it means:**  
Scheduler cannot place the pod on any node.

**How to troubleshoot & fix:**
- Describe pod and check events
- Look for insufficient CPU/memory
- Verify node availability
- Check node selectors, taints, and tolerations
- Verify PVC is bound
- Add nodes or adjust resource requests

---

## Scenario 6: OOMKilled  
**What it means:**  
Container exceeded its memory limit and was killed.

**How to troubleshoot & fix:**
- Check pod status for `OOMKilled`
- Review memory usage
- Increase memory limits
- Optimize application memory usage
- Add proper resource requests and limits
- Monitor memory usage continuously

---

## Scenario 7: Pod restarts frequently  
**What it means:**  
Application starts but keeps restarting.

**How to troubleshoot & fix:**
- Check container logs
- Inspect liveness probes
- Verify startup time vs probe delay
- Check application crashes or dependency failures
- Fix probes or application logic
- Redeploy after stabilization

---

## Scenario 8: Exit Code 1  
**What it means:**  
Container exited due to an application-level error.

**How to troubleshoot & fix:**
- Inspect logs to identify failure reason
- Validate startup script or command
- Check environment variables and secrets
- Verify file paths and permissions
- Fix application error and redeploy

---

## Scenario 9: Deployment created, but no pod started  
**What it means:**  
Deployment exists but pods are not scheduled or created.

**How to troubleshoot & fix:**
- Check deployment conditions
- Verify replica count
- Ensure selector labels match pod labels
- Check namespace mismatch
- Review admission controller or policy restrictions
- Fix deployment configuration

---

## Scenario 10: Pod Created but Init Container skipped  
**What it means:**  
Init container does not run as expected.

**How to troubleshoot & fix:**
- Verify init container definition
- Check init container logs
- Ensure correct image and command
- Validate dependencies required by init container
- Fix configuration and redeploy
- Remember: init containers must succeed before main container starts

---

## Scenario 11: Wrap-up & Best Practices  
**Key advice to prevent deployment failures:**
- Always check pod events and logs first
- Use resource requests and limits
- Validate manifests before applying
- Maintain environment parity (dev/stage/prod)
- Use proper monitoring and alerting
- Automate checks using CI/CD pipelines
- Document known failure patterns and fixes

---

## Question 11: InitContainer Failing (CrashLoopBackOff)

**Problem:**  
InitContainer fails repeatedly and blocks the main container.

**Troubleshooting & Resolution:**
- Check init container logs using `kubectl logs <pod> -c <init-container>`
- Describe pod to inspect events
- Verify init container image and command
- Check dependencies like DB, API, or file system access
- Validate secrets and configmaps used by init container
- Fix failure and redeploy  
Note: Main container will not start until init container succeeds.

---

## Question 12: Sidecar Pattern Logging Issue

**Problem:**  
Application runs, but logs are not collected by the sidecar container.

**Troubleshooting & Resolution:**
- Verify shared volume between app and sidecar
- Ensure log file paths match in both containers
- Check sidecar container logs
- Confirm file permissions on shared volume
- Validate log rotation configuration
- Fix volume mounts or permissions and redeploy

---

## Question 13: Pod Affinity Causing Latency

**Problem:**  
Pod affinity rules increase latency due to poor pod placement.

**Troubleshooting & Resolution:**
- Review pod affinity and anti-affinity rules
- Check node distribution of pods
- Identify over-constrained scheduling rules
- Relax affinity rules if possible
- Use topology spread constraints
- Balance performance and availability

---

## Question 14: Pod Not Receiving IP (CNI Troubleshoot)

**Problem:**  
Pod is created but does not get an IP address.

**Troubleshooting & Resolution:**
- Check pod events for CNI errors
- Inspect CNI plugin pods (Calico, Cilium, Flannel)
- Verify node has available IP addresses
- Check CNI configuration files
- Restart CNI pods if required
- Fix CNI issues and reschedule pod

---

## Question 15: ReplicaSet Not Creating Pods

**Problem:**  
ReplicaSet exists but pods are not created.

**Troubleshooting & Resolution:**
- Check ReplicaSet status and events
- Verify replica count
- Ensure selector labels match pod template labels
- Check admission controllers or policies
- Validate resource availability
- Correct configuration and reapply

---

## Question 16: Deployment Rollback Not Working

**Problem:**  
Rollback command executes but application does not revert.

**Troubleshooting & Resolution:**
- Check rollout history
- Verify previous revision exists
- Confirm `revisionHistoryLimit` is not too low
- Check if deployment is paused
- Validate image and configuration differences
- Fix rollout settings and retry rollback

---

## Question 17: Paused Deployment Stuck

**Problem:**  
Deployment remains paused and does not proceed.

**Troubleshooting & Resolution:**
- Check deployment status for paused condition
- Resume deployment using rollout resume
- Review CI/CD pipeline logic
- Ensure no manual pause was left unintentionally
- Monitor rollout progress after resume

---

## Question 18: Blue-Green Traffic Still Routed to Old Pods

**Problem:**  
Traffic continues hitting old version after blue-green deployment.

**Troubleshooting & Resolution:**
- Verify service selector labels
- Check ingress or load balancer routing rules
- Confirm new pods are ready
- Update service to point to new version
- Validate DNS or cache behavior
- Switch traffic cleanly and monitor

---

## Question 19: Canary Pods Receiving All Traffic

**Problem:**  
Canary pods receive 100% traffic instead of partial traffic.

**Troubleshooting & Resolution:**
- Check ingress or service routing rules
- Validate traffic weight configuration
- Ensure labels are correct
- Review service mesh configuration (Istio/Linkerd)
- Fix routing rules to split traffic properly
- Monitor traffic distribution

---

## Question 20: Image Update Ignored (No Rollout Triggered)

**Problem:**  
New image is pushed but deployment does not restart.

**Troubleshooting & Resolution:**
- Verify image tag is updated
- Avoid using `latest` tag
- Check imagePullPolicy
- Confirm deployment spec change occurred
- Force rollout restart if needed
- Use immutable image tags for deployments

---

## Question 21: Deployment scaled but missing replicas

**Problem:**  
Deployment shows desired replicas increased, but actual running pods are fewer.

**Troubleshooting & Resolution:**
- Check deployment status and conditions
- Describe pods to inspect scheduling events
- Look for insufficient CPU or memory errors
- Verify node availability and readiness
- Check PodDisruptionBudgets blocking scale-up
- Validate resource requests and limits
- Add nodes or adjust resource configuration

---

## Question 22: Downtime during rolling update

**Problem:**  
Users experience downtime while rolling updates are in progress.

**Troubleshooting & Resolution:**
- Check rolling update strategy configuration
- Verify maxUnavailable and maxSurge values
- Ensure readiness probes are configured correctly
- Confirm old pods are not terminated before new pods become ready
- Check load balancer and service health checks
- Adjust rollout strategy to ensure zero-downtime deployments

---

## Question 23: ClusterIP unreachable inside cluster

**Problem:**  
Service ClusterIP cannot be accessed from within the cluster.

**Troubleshooting & Resolution:**
- Verify service exists and is in correct namespace
- Check service selector labels match pod labels
- Inspect service endpoints
- Verify kube-proxy is running on nodes
- Check NetworkPolicies blocking traffic
- Fix selectors or networking rules

---

## Question 24: ClusterIP resolves but connection refused

**Problem:**  
Service DNS resolves, but connection is refused.

**Troubleshooting & Resolution:**
- Check container is listening on correct port
- Verify targetPort matches containerPort
- Inspect pod logs for application startup issues
- Check readiness probe failures
- Validate firewall or network policy rules
- Fix port mappings or application config

---

## Question 25: NodePort works on one node only

**Problem:**  
NodePort service is reachable only via one node IP.

**Troubleshooting & Resolution:**
- Check if pods are running on multiple nodes
- Verify kube-proxy configuration
- Ensure external traffic policy is correctly set
- Check node firewall or security group rules
- Confirm all nodes allow NodePort traffic
- Fix networking or security configuration

---

## Question 26: NodePort not accessible externally

**Problem:**  
NodePort service cannot be accessed from outside the cluster.

**Troubleshooting & Resolution:**
- Verify NodePort range is open on firewall
- Check cloud security groups or NACLs
- Ensure correct node IP is used
- Validate service type is NodePort
- Confirm application is listening on correct port
- Fix external access rules

---

## Question 27: Traffic going to pods on one node only

**Problem:**  
All traffic is routed to pods on a single node.

**Troubleshooting & Resolution:**
- Check service load balancing behavior
- Verify pod distribution across nodes
- Check session affinity settings
- Inspect externalTrafficPolicy configuration
- Validate ingress or load balancer setup
- Adjust service or traffic policy

---

## Question 28: Service works via Pod IP, not Service name

**Problem:**  
Application is reachable using pod IP but not via service DNS name.

**Troubleshooting & Resolution:**
- Verify service DNS name and namespace
- Check CoreDNS pod health
- Inspect service endpoints
- Validate service selector labels
- Test DNS resolution inside the pod
- Fix service or DNS configuration

---

## Question 29: Headless service returns no DNS records

**Problem:**  
Headless service does not return DNS entries.

**Troubleshooting & Resolution:**
- Verify service is defined with clusterIP: None
- Check pod readiness status
- Ensure pods match service selector
- Validate StatefulSet configuration
- Check CoreDNS logs
- Fix service or pod labels

---

## Question 30: Pods stuck in ContainerCreating

**Problem:**  
Pods remain in ContainerCreating state for long time.

**Troubleshooting & Resolution:**
- Describe pod to inspect events
- Check image pull status
- Verify volume mounts and PVC binding
- Inspect CNI plugin health
- Check node disk pressure
- Resolve underlying issue and reschedule pod

---

✅ **This document is ideal for Kubernetes interviews, real-time troubleshooting, and DevOps/SRE preparation.**

---

## Author
**Velanati Naveen Kumar**
- DevOps Engineer  
- CI/CD | AWS | Kubernetes | Terraform | GitOps | Automation
- Connect with me: [LinkedIn](https://www.linkedin.com/in/naveenvelanati/)
- 📞 +91 9848545101
