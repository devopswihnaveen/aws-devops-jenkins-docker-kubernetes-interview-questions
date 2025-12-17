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
