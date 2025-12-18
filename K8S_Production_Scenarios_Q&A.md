# Kubernetes Production Scenarios – Interview Questions & Answers (Complete Guide)

---

## 1. Your application pod keeps restarting. How do you troubleshoot it step by step?

**Answer:**
1. Check pod status and restart count  
2. Inspect pod logs using `kubectl logs`
3. Describe pod to view events
4. Check exit codes and error messages
5. Verify environment variables and configs
6. Inspect liveness/readiness probes
7. Check resource limits (CPU/memory)
8. Fix root cause and redeploy

---

## 2. A pod is in `CrashLoopBackOff`. What are the common causes and fixes?

**Common Causes:**
- Application crash on startup
- Wrong command or entrypoint
- Missing config or secret
- Aggressive liveness probe
- Insufficient memory (OOM)

**Fixes:**
- Check logs and events
- Fix app/config issues
- Adjust probes
- Increase resources if required

---

## 3. How do you debug a pod that works in dev but fails in production?

**Answer:**
- Compare environment variables and secrets
- Verify image version and dependencies
- Check resource limits differences
- Validate external services (DB, APIs)
- Check network policies and firewalls
- Compare data size and formats
- Ensure environment parity

---

## 4. Your container starts slowly and gets killed. How do you handle startup issues?

**Answer:**
- Increase `initialDelaySeconds` in probes
- Use startupProbe (if supported)
- Optimize application startup logic
- Allocate sufficient CPU/memory
- Separate initialization logic into init containers

---

## 5. How do readiness and liveness probes help during deployments?

**Answer:**
- **Readiness probe** ensures traffic goes only to ready pods
- **Liveness probe** restarts unhealthy pods
- Prevents traffic to broken pods
- Enables zero-downtime deployments
- Improves application reliability

---

## 6. When would you use an init container in real projects?

**Answer:**
- Database migrations
- Waiting for external services
- Pre-loading data or configs
- Permission setup for volumes
- Any task that must complete before app starts

---

## 7. One container in a multi-container pod fails. What happens and how do you debug?

**Answer:**
- Pod may restart depending on restart policy
- Other containers may continue running
- Debug by checking logs of failing container
- Inspect shared volumes and dependencies
- Fix configuration or application error

---

## 8. How do you handle application configuration changes without restarting pods?

**Answer:**
- Use ConfigMaps mounted as volumes
- Enable application hot reload
- Use external configuration services
- For env var changes, rollout restart is required

---

# Deployments, Rollouts & Zero Downtime

## 9. How do you ensure zero-downtime deployments in Kubernetes?

**Answer:**
- Use RollingUpdate strategy
- Configure readiness probes
- Set proper maxUnavailable and maxSurge
- Use multiple replicas
- Validate load balancer health checks

---

## 10. A new deployment caused production issues. How do you rollback safely?

**Answer:**
- Check rollout history
- Rollback to previous stable version
- Monitor application health
- Validate logs and metrics
- Fix issue before redeploying

---

## 11. Difference between rolling update and recreate strategy—when do you use each?

**Answer:**
- **Rolling Update:** Gradual pod replacement, zero downtime (default)
- **Recreate:** All pods terminated before new ones start (used when versions are incompatible)

---

## 12. How do you control how many pods go down during deployment?

**Answer:**
- Configure `maxUnavailable`
- Configure `maxSurge`
- Use PodDisruptionBudgets
- Proper probe configuration

---

## 13. How do you deploy database-related changes along with application updates?

**Answer:**
- Run migrations using init containers or jobs
- Use backward-compatible schema changes
- Apply DB changes before app rollout
- Roll out app gradually

---

## 14. How do you use canary deployments in Kubernetes?

**Answer:**
- Deploy a small subset of new version pods
- Route partial traffic to canary
- Monitor metrics and logs
- Gradually increase traffic
- Promote or rollback based on results

---

## 15. What happens if a deployment gets stuck midway?

**Answer:**
- Some pods updated, others not
- Caused by failing probes or resource issues
- Inspect deployment conditions
- Fix failing pods
- Resume or rollback deployment

---

# Services, Networking & Ingress

## 16. Pods are running but the application is not accessible. How do you troubleshoot?

**Answer:**
- Check service configuration
- Verify selectors and endpoints
- Validate pod ports
- Check ingress or load balancer
- Inspect network policies and firewall rules

---

## 17. Difference between ClusterIP, NodePort, and LoadBalancer with real use cases?

**Answer:**
- **ClusterIP:** Internal services (DB, backend)
- **NodePort:** Testing or limited external access
- **LoadBalancer:** Production external access

---

## 18. How does Kubernetes service discovery work internally?

**Answer:**
- Services get virtual IPs
- CoreDNS resolves service names
- Traffic load-balanced across endpoints
- Uses kube-proxy rules

---

## 19. How do you expose multiple services using a single load balancer?

**Answer:**
- Use Ingress
- Path-based or host-based routing
- Single external IP
- Reduces cost and complexity

---

## 20. What happens if an ingress controller pod goes down?

**Answer:**
- Traffic disruption may occur
- If replicas exist, traffic shifts automatically
- Ensure multiple replicas
- Use health checks and monitoring

---

## 21. How do you handle TLS/SSL certificates in Kubernetes?

**Answer:**
- Store certs as secrets
- Configure TLS in ingress
- Use cert-manager for automation
- Enable auto-renewal

---

# ConfigMaps, Secrets & Security

## 22. How do you manage secrets securely in Kubernetes?

**Answer:**
- Use Kubernetes Secrets
- Integrate with external secret managers
- Restrict access using RBAC
- Avoid hardcoding secrets
- Rotate secrets periodically

---

## 23. What happens if a secret or ConfigMap is updated—do pods get updated automatically?

**Answer:**
- Volume-mounted updates reflect automatically
- Environment variable updates require pod restart
- Some apps require reload logic

---

## 24. How do you restrict pod-to-pod communication?

**Answer:**
- Use NetworkPolicies
- Define allowed ingress/egress rules
- Implement zero-trust networking
- Monitor traffic patterns

---

## 25. How do RBAC roles differ for developers vs DevOps engineers?

**Answer:**
- **Developers:** Access to pods, logs, deployments
- **DevOps:** Full cluster, nodes, networking, security
- Enforce least-privilege principle

---

# Scaling, Performance & Reliability

## 26. How does HPA work and what metrics have you used in real projects?

**Answer:**
- Scales pods based on metrics
- Common metrics: CPU, memory
- Custom metrics: requests/sec, latency
- Requires Metrics Server or Prometheus

---

## 27. Pods are not scaling even though traffic increased. How do you debug?

**Answer:**
- Check HPA status
- Verify metrics availability
- Inspect resource requests
- Validate scaling thresholds
- Check max/min replica limits

---

## 28. How do you handle node failures in production?

**Answer:**
- Kubernetes reschedules pods automatically
- Use multiple nodes and AZs
- Enable cluster autoscaler
- Use PodDisruptionBudgets
- Monitor node health

---

## 29. How do you control resource usage to avoid noisy neighbor problems?

**Answer:**
- Set CPU and memory requests/limits
- Use namespaces with quotas
- Implement HPA/VPA
- Monitor resource usage

---

## 30. How do you monitor Kubernetes cluster and application health?

**Answer:**
- Use Prometheus and Grafana
- Monitor node, pod, and app metrics
- Centralized logging (ELK, Loki)
- Set alerts for failures and latency
- Track SLOs and SLAs

---

