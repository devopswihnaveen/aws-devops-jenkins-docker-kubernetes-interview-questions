
# Kubernetes Deployments - Complete Q&A Guide

## Deployments

### 1. What is a Kubernetes Deployment?
A Deployment is a higher-level abstraction that manages ReplicaSets and provides declarative updates for Pods and ReplicaSets.

### 2. How do you create a Deployment?
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
    name: nginx-deployment
spec:
    replicas: 3
    selector:
        matchLabels:
            app: nginx
    template:
        metadata:
            labels:
                app: nginx
        spec:
            containers:
            - name: nginx
                image: nginx:1.14.2
                ports:
                - containerPort: 80
```

### 3. What are Deployment strategies?
- **Recreate**: Terminates all pods then creates new ones
- **RollingUpdate**: Gradually replaces pods (default)

### 4. How do you rollout updates in a Deployment?
Using `kubectl set image` or by updating the deployment spec and applying it.

### 5. What is a rollback in Kubernetes?
Reverting to a previous Deployment revision using `kubectl rollout undo`.

### 6. How do you check Deployment status?
`kubectl rollout status deployment/nginx-deployment`

### 7. What is maxSurge in RollingUpdate?
Maximum number of pods that can be created above desired replicas during update.

### 8. What is maxUnavailable in RollingUpdate?
Maximum number of pods that can be unavailable during update.

### 9. How do you scale a Deployment?
`kubectl scale deployment nginx-deployment --replicas=5`

### 10. What triggers a new rollout?
Changing pod template spec (image, env vars, resource limits, etc.).

## ReplicaSets

### 11. What is a ReplicaSet?
A controller that ensures a specified number of pod replicas are running at all times.

### 12. Difference between ReplicaSet and Deployment?
Deployments manage ReplicaSets; ReplicaSets don't manage updates.

### 13. How do you create a ReplicaSet?
```yaml
apiVersion: apps/v1
kind: ReplicaSet
metadata:
    name: nginx-rs
spec:
    replicas: 3
    selector:
        matchLabels:
            app: nginx
    template:
        metadata:
            labels:
                app: nginx
        spec:
            containers:
            - name: nginx
                image: nginx:latest
```

### 14. Can you manually edit a ReplicaSet?
Yes, but Deployments are preferred for managing ReplicaSets.

### 15. What happens when you delete a ReplicaSet?
Pods are also deleted by default (can use `--cascade=orphan` to keep pods).

## Replication Controller

### 16. What is a Replication Controller?
Legacy controller that ensures pod replicas; replaced by ReplicaSet.

### 17. Difference between ReplicaSet and Replication Controller?
ReplicaSets support set-based selectors; Replication Controllers use equality-based selectors.

### 18. Why use ReplicaSets over Replication Controllers?
Better selector support and used by Deployments.

### 19. How do you convert Replication Controller to ReplicaSet?
Change `kind` from `ReplicationController` to `ReplicaSet` and use set-based selectors.

### 20. What is the selector in Replication Controller?
Simple key-value label matching (equality-based).

## DaemonSets

### 21. What is a DaemonSet?
Ensures a pod runs on every node (or selected nodes) in the cluster.

### 22. Use cases for DaemonSet?
Logging agents, monitoring agents, network plugins (Flannel, Calico).

### 23. How do you create a DaemonSet?
```yaml
apiVersion: apps/v1
kind: DaemonSet
metadata:
    name: fluentd-elasticsearch
spec:
    selector:
        matchLabels:
            name: fluentd-elasticsearch
    template:
        metadata:
            labels:
                name: fluentd-elasticsearch
        spec:
            containers:
            - name: fluentd-elasticsearch
                image: fluent/fluentd-kubernetes-daemonset:elasticsearch
```

### 24. Can DaemonSet pods have node selectors?
Yes, using `nodeSelector` or `affinity`.

### 25. What happens when a new node joins the cluster?
DaemonSet automatically schedules a pod on the new node.

## StatefulSets

### 26. What is a StatefulSet?
Manages stateful applications with stable identity, persistent storage, and ordered deployment.

### 27. Difference between Deployment and StatefulSet?
StatefulSets provide stable hostnames, ordered scaling, persistent storage.

### 28. What are StatefulSet components?
- Pods with stable identities (nginx-0, nginx-1, nginx-2)
- Headless Service
- PersistentVolumeClaim

### 29. How do you create a StatefulSet?
```yaml
apiVersion: apps/v1
kind: StatefulSet
metadata:
    name: mysql
spec:
    serviceName: mysql
    replicas: 3
    selector:
        matchLabels:
            app: mysql
    template:
        metadata:
            labels:
                app: mysql
        spec:
            containers:
            - name: mysql
                image: mysql:5.7
                volumeMounts:
                - name: data
                    mountPath: /var/lib/mysql
    volumeClaimTemplates:
    - metadata:
            name: data
        spec:
            accessModes: ["ReadWriteOnce"]
            resources:
                requests:
                    storage: 1Gi
```

### 30. What is a Headless Service?
Service without ClusterIP, used by StatefulSets for stable network identity.

### 31. How does ordinal index work in StatefulSet?
Pods are numbered 0 to N-1; scale up/down follows order.

### 32. Can StatefulSet pods be rescheduled?
Only if node fails; they maintain identity and storage.

### 33. What is volumeClaimTemplates?
Templates for creating PersistentVolumeClaims for each pod.

### 34. How do you update StatefulSet?
Using `OnDelete` (manual) or `RollingUpdate` (automatic) strategy.

### 35. Use cases for StatefulSet?
Databases (MySQL, PostgreSQL), message queues (RabbitMQ, Kafka), distributed systems.

## kube-system Namespace Components

### 36. What is kube-system namespace?
Default namespace for Kubernetes system components.

### 37. What is kube-apiserver?
Core API server managing cluster API requests.

### 38. What is kube-controller-manager?
Runs all controller processes (Deployment, StatefulSet, DaemonSet controllers).

### 39. What is kube-scheduler?
Assigns pods to nodes based on resource requests and constraints.

### 40. What is etcd?
Distributed key-value store storing cluster state.

### 41. What is kube-proxy?
Network proxy maintaining network rules on each node.

### 42. What is CoreDNS?
DNS service for service discovery within the cluster.

### 43. What are network plugins (CNI)?
Flannel, Calico, Weave for pod networking.

### 44. What is kubelet?
Node agent ensuring containers run in pods.

### 45. How do you view kube-system components?
`kubectl get pods -n kube-system`

### 46. What is control-plane node?
Node running apiserver, scheduler, controller-manager.

### 47. What are static pods?
Pods managed by kubelet without API server (control-plane components).

### 48. How do you check component logs?
`kubectl logs -n kube-system <pod-name>` or `/var/log/pods/`

### 49. What is a PodDisruptionBudget?
Ensures pod availability during voluntary disruptions.

### 50. What is kubectl drain?
Evicts pods from a node for maintenance.

### 51. How do you add custom controller?
Deploy custom controller pod/Deployment in kube-system namespace.

### 52. What is RBAC in kube-system?
Role-based access control for system components using ServiceAccounts.

## Node Groups and Scheduling

### 53. What are Readiness Probes?
Readiness probes determine if a pod is ready to accept traffic. If a pod fails its readiness probe, it is removed from the service endpoints.

### 54. What are Liveness Probes?
Liveness probes check if a pod is still running. If a liveness probe fails, Kubernetes will restart the pod.

### 55. What is a Taint?
A taint is a property applied to a node that prevents pods from being scheduled on it unless they tolerate the taint.

### 56. What are Tolerations?
Tolerations are applied to pods and allow them to be scheduled on nodes with matching taints.

### 57. What is Node Affinity?
Node affinity is a set of rules that constrain which nodes your pod can be scheduled on based on node labels.

### 58. What is Node Anti-Affinity?
Node anti-affinity prevents a pod from being scheduled on a node if that node is already running a pod with a specific label.

### 59. What is Pod Affinity?
Pod affinity allows you to specify that a pod should be scheduled on the same node as another pod.

### 60. What is Pod Anti-Affinity?
Pod anti-affinity prevents a pod from being scheduled on the same node as another pod with a specific label.

### 61. What is Cordon?
Cordon marks a node as unschedulable, preventing new pods from being scheduled on it.

### 62. What is Uncordon?
Uncordon marks a node as schedulable again, allowing new pods to be scheduled on it.

## Definitions and Troubleshooting

### 63. What is a Pod?
A Pod is the smallest deployable unit in Kubernetes, representing a single instance of a running process in your cluster.

### 64. What is a Service?
A Service is an abstraction that defines a logical set of Pods and a policy by which to access them, often used to expose applications.

### 65. What is a Namespace?
Namespaces are a way to divide cluster resources between multiple users or applications, providing a scope for names.

### 66. What is a ConfigMap?
A ConfigMap is an API object used to store non-confidential data in key-value pairs, allowing you to separate configuration from application code.

### 67. What is a Secret?
A Secret is similar to a ConfigMap but is intended to hold sensitive information, such as passwords or tokens.

### 68. How do you troubleshoot a failing Pod?
Use `kubectl describe pod <pod-name>` to get detailed information about the pod's status and events, and `kubectl logs <pod-name>` to check the logs.

### 69. What is a CrashLoopBackOff?
A CrashLoopBackOff occurs when a Pod fails to start repeatedly, causing Kubernetes to back off and wait before trying to restart it again.

### 70. How do you check resource usage of Pods?
Use `kubectl top pods` to view the resource usage of Pods in the cluster.

### 71. What is a Node Condition?
Node Conditions are a set of conditions that describe the health of a node, such as Ready, OutOfDisk, and MemoryPressure.

### 72. How do you drain a node?
Use `kubectl drain <node-name>` to safely evict all Pods from a node for maintenance.

### 73. What is a Persistent Volume (PV)?
A Persistent Volume is a piece of storage in the cluster that has been provisioned by an administrator or dynamically provisioned using Storage Classes.

### 74. What is a Persistent Volume Claim (PVC)?
A Persistent Volume Claim is a request for storage by a user, which can be fulfilled by a Persistent Volume.

### 75. How do you view events in a namespace?
Use `kubectl get events -n <namespace>` to view events related to resources in a specific namespace.

### 76. What is a ResourceQuota?
A ResourceQuota is a limit on the amount of resources (CPU, memory, etc.) that can be consumed by a namespace.

### 77. How do you check the status of a Deployment?
Use `kubectl get deployments` to view the status of all deployments in the current namespace.

### 78. What is a Horizontal Pod Autoscaler?
A Horizontal Pod Autoscaler automatically scales the number of Pods in a Deployment or ReplicaSet based on observed CPU utilization or other select metrics.

### 79. How do you update a ConfigMap?
You can update a ConfigMap using `kubectl apply -f <configmap-file.yaml>` or `kubectl edit configmap <configmap-name>`.

### 80. What is a Helm Chart?
A Helm Chart is a package of pre-configured Kubernetes resources that can be easily deployed and managed.


### 81. What is the Pending pod status?
Pending means the pod has been created but not yet scheduled on a node. Common causes: insufficient resources, node selectors not matching, or persistent volume not available.

**Troubleshooting:**
```bash
kubectl describe pod <pod-name>
kubectl get events -n <namespace>
```

**Resolution:** Check node resources, verify node selectors, ensure PVCs are bound, or add more nodes to the cluster.

### 82. What causes CrashLoopBackOff?
CrashLoopBackOff occurs when a container repeatedly crashes and Kubernetes restarts it with exponential backoff delays.

**Common causes:**
- Application errors or exit codes
- Missing environment variables
- Incorrect configuration
- Dependency not available
- Resource limits exceeded

**Troubleshooting:**
```bash
kubectl logs <pod-name>
kubectl logs <pod-name> --previous
kubectl describe pod <pod-name>
```

**Resolution:** Fix application code, verify configuration, add missing dependencies, increase resource limits.

### 83. What is ImagePullBackOff?
ImagePullBackOff means Kubernetes cannot pull the container image from the registry.

**Common causes:**
- Incorrect image name or tag
- Image doesn't exist in registry
- Registry credentials missing
- Registry is unreachable
- Private image without imagePullSecrets

**Troubleshooting:**
```bash
kubectl describe pod <pod-name>
kubectl get events -n <namespace>
```

**Resolution:** Verify image name/tag, add imagePullSecrets for private registries, check registry connectivity, ensure credentials are correct.

### 84. What is ImageError?
ImageError occurs when the image exists but cannot be used (e.g., wrong architecture, corrupted image).

**Common causes:**
- Image architecture mismatch (ARM vs x86)
- Corrupted or invalid image
- Image is not a valid container image

**Troubleshooting:**
```bash
kubectl describe pod <pod-name>
```

**Resolution:** Use correct image architecture, rebuild the image, verify image integrity.

### 85. What is Restart policy in Pods?
Restart policy defines what Kubernetes should do when a container exits.

**Types:**
- `Always`: Always restart (default)
- `OnFailure`: Restart only on non-zero exit code
- `Never`: Never restart

**Example:**
```yaml
spec:
    restartPolicy: OnFailure
    containers:
    - name: app
        image: myapp:1.0
```

### 86. What causes pod restart loops?
Pod restart loops occur when containers fail immediately after starting.

**Common causes:**
- Application crashes on startup
- Missing required files or directories
- Incorrect startup command
- Liveness probe failing immediately

**Resolution:** Check application logs, verify startup command, adjust liveness probe delays, add init containers for setup.

### 87. How do you debug pod status issues?
```bash
# Get pod status overview
kubectl get pods -o wide

# Detailed pod information
kubectl describe pod <pod-name>

# Check logs
kubectl logs <pod-name>
kubectl logs <pod-name> --previous

# Check events
kubectl get events -n <namespace> --sort-by='.lastTimestamp'

# Check resource availability
kubectl top nodes
kubectl top pods
```

### 88. What is an Init Container?
Init containers run before app containers and can be used to set up prerequisites.

**Use case for troubleshooting:**
```yaml
spec:
    initContainers:
    - name: wait-for-service
        image: busybox
        command: ['sh', '-c', 'until nslookup database; do echo waiting; sleep 2; done']
    containers:
    - name: app
        image: myapp:1.0
```

### 89. How do you check if a Pod is ready?
```bash
kubectl get pods -o jsonpath='{.items[*].status.conditions[?(@.type=="Ready")].status}'
kubectl wait --for=condition=ready pod <pod-name> --timeout=300s
```

### 90. What is a liveness vs readiness probe failure?
- **Liveness probe failure:** Pod is restarted
- **Readiness probe failure:** Pod is removed from service endpoints but not restarted

**Example:**
```yaml
livenessProbe:
    httpGet:
        path: /health
        port: 8080
    initialDelaySeconds: 30
    periodSeconds: 10

readinessProbe:
    httpGet:
        path: /ready
        port: 8080
    initialDelaySeconds: 5
    periodSeconds: 5
```

## ConfigMaps and Secrets

### 91. What is a ConfigMap?
A ConfigMap is an API object that stores non-confidential configuration data in key-value pairs, allowing you to decouple configuration from application code.

### 92. How do you create a ConfigMap?
```yaml
apiVersion: v1
kind: ConfigMap
metadata:
    name: app-config
data:
    database.url: "postgres://db:5432"
    log.level: "info"
    app.properties: |
        key1=value1
        key2=value2
```

Or via command: `kubectl create configmap app-config --from-literal=key=value`

### 93. How do you mount a ConfigMap in a Pod?
```yaml
spec:
    containers:
    - name: app
        image: myapp:1.0
        envFrom:
        - configMapRef:
            name: app-config
        volumeMounts:
        - name: config
            mountPath: /etc/config
    volumes:
    - name: config
        configMap:
            name: app-config
```

### 94. What is a Secret?
A Secret is similar to ConfigMap but designed to store sensitive data like passwords, tokens, and API keys, with base64 encoding.

### 95. Types of Secrets?
- `Opaque`: Default; stores arbitrary user-defined data
- `kubernetes.io/service-account-token`: Service account token
- `kubernetes.io/dockercfg`: Serialized Docker config
- `kubernetes.io/dockerconfigjson`: Docker config JSON
- `kubernetes.io/basic-auth`: Basic authentication
- `kubernetes.io/ssh-auth`: SSH authentication
- `kubernetes.io/tls`: TLS certificate and key
- `bootstrap.kubernetes.io/token`: Bootstrap token

### 96. How do you create a Secret?
```yaml
apiVersion: v1
kind: Secret
metadata:
    name: db-secret
type: Opaque
stringData:
    username: admin
    password: mysecretpassword
```

Or via command: `kubectl create secret generic db-secret --from-literal=username=admin --from-literal=password=pass`

### 97. How do you mount a Secret in a Pod?
```yaml
spec:
    containers:
    - name: app
        image: myapp:1.0
        env:
        - name: DB_USER
            valueFrom:
                secretKeyRef:
                    name: db-secret
                    key: username
        - name: DB_PASS
            valueFrom:
                secretKeyRef:
                    name: db-secret
                    key: password
```

### 98. Difference between ConfigMap and Secret?
- ConfigMap: Non-confidential data, not encrypted
- Secret: Sensitive data, base64 encoded (should be encrypted at rest)

### 99. How do you update a ConfigMap without restarting pods?
Update the ConfigMap; pods using volume mounts see changes, but env vars require restart. Use `kubectl rollout restart deployment/<name>` to restart.

### 100. Can you use Secrets with environment variables?
Yes, but it's less ideal than volume mounts since env vars are set at container creation and don't update automatically.

## Volumes and Storage

### 101. What is a Volume?
A Volume is storage attached to a Pod that persists for the Pod's lifetime, allowing containers to share data.

### 102. Types of Volumes?
- `emptyDir`: Temporary storage
- `hostPath`: Node filesystem
- `configMap`: ConfigMap data
- `secret`: Secret data
- `persistentVolumeClaim`: PVC
- `nfs`: Network File System
- `awsElasticBlockStore`: AWS EBS
- `gcePersistentDisk`: Google Compute Disk
- `azureDisk`: Azure Disk

### 103. What is emptyDir Volume?
Empty directory created when Pod is created; destroyed when Pod is deleted. Useful for temporary data and multi-container communication.

```yaml
spec:
    containers:
    - name: container1
        image: myapp:1.0
        volumeMounts:
        - name: cache
            mountPath: /tmp/cache
    volumes:
    - name: cache
        emptyDir: {}
```

### 104. What is hostPath Volume?
Mounts a file or directory from the host node's filesystem into the Pod.

```yaml
volumes:
- name: host-logs
    hostPath:
        path: /var/log
        type: Directory
```

### 105. What is a Persistent Volume (PV)?
A Persistent Volume is a piece of storage in the cluster provisioned by an administrator or dynamically provisioned, with a lifecycle independent of Pods.

### 106. How do you create a Persistent Volume?
```yaml
apiVersion: v1
kind: PersistentVolume
metadata:
    name: pv-storage
spec:
    capacity:
        storage: 10Gi
    accessModes:
    - ReadWriteOnce
    persistentVolumeReclaimPolicy: Retain
    storageClassName: standard
    nfs:
        server: 192.168.1.100
        path: "/exported/data"
```

### 107. What is a Persistent Volume Claim (PVC)?
A PersistentVolumeClaim is a user's request for storage; Kubernetes binds it to a PV that satisfies the request.

### 108. How do you create a Persistent Volume Claim?
```yaml
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
    name: my-pvc
spec:
    accessModes:
    - ReadWriteOnce
    storageClassName: standard
    resources:
        requests:
            storage: 5Gi
```

### 109. What are access modes for PV/PVC?
- `ReadWriteOnce` (RWO): Mounted as read-write by a single node
- `ReadOnlyMany` (ROX): Mounted as read-only by many nodes
- `ReadWriteMany` (RWX): Mounted as read-write by many nodes

### 110. What is persistentVolumeReclaimPolicy?
Defines what happens to the PV when the PVC is deleted.

- `Retain`: Keep the PV; manual cleanup required
- `Delete`: Automatically delete the PV
- `Recycle`: Deprecated; scrubs the PV

### 111. What is a Storage Class?
A StorageClass enables dynamic provisioning of PersistentVolumes based on provisioner type and parameters.

### 112. How do you create a Storage Class?
```yaml
apiVersion: storage.k8s.io/v1
kind: StorageClass
metadata:
    name: fast-storage
provisioner: kubernetes.io/aws-ebs
parameters:
    type: gp2
    iops: "1000"
    encrypted: "true"
allowVolumeExpansion: true
```

### 113. How do you use a Storage Class in a PVC?
```yaml
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
    name: my-pvc
spec:
    storageClassName: fast-storage
    accessModes:
    - ReadWriteOnce
    resources:
        requests:
            storage: 10Gi
```

### 114. What is dynamic provisioning?
Automatic creation of PVs based on PVC requests using a Storage Class and provisioner.

### 115. How do you expand a PVC?
Update the `storage` request in the PVC spec; the PV will expand if `allowVolumeExpansion: true` in Storage Class.

```bash
kubectl patch pvc my-pvc -p '{"spec":{"resources":{"requests":{"storage":"20Gi"}}}}'
```

### 116. What causes PVC to be in Pending state?
- No available PV matching the claim
- Storage Class provisioner not available
- Insufficient storage capacity
- Access mode mismatch

**Troubleshooting:**
```bash
kubectl describe pvc <pvc-name>
kubectl get pv
kubectl get storageclass
```

### 117. How do you check PV and PVC status?
```bash
kubectl get pv
kubectl get pvc
kubectl describe pv <pv-name>
kubectl describe pvc <pvc-name>
```

### 118. What happens when you delete a PVC?
If `persistentVolumeReclaimPolicy` is `Delete`, the PV is deleted. If `Retain`, the PV remains and must be manually deleted.

## Horizontal Pod Autoscaler (HPA)

### 119. What is a Horizontal Pod Autoscaler?
HPA automatically scales the number of Pods in a Deployment or ReplicaSet based on observed metrics like CPU utilization or custom metrics.

### 120. How do you create an HPA?
```yaml
apiVersion: autoscaling/v2
kind: HorizontalPodAutoscaler
metadata:
    name: app-hpa
spec:
    scaleTargetRef:
        apiVersion: apps/v1
        kind: Deployment
        name: app-deployment
    minReplicas: 2
    maxReplicas: 10
    metrics:
    - type: Resource
        resource:
            name: cpu
            target:
                type: Utilization
                averageUtilization: 70
    - type: Resource
        resource:
            name: memory
            target:
                type: Utilization
                averageUtilization: 80
```

### 121. What metrics does HPA use?
- CPU utilization (requires metrics-server)
- Memory utilization
- Custom metrics (from monitoring systems)
- External metrics

### 122. What is metrics-server?
A cluster component that collects resource metrics from Kubelets and exposes them via the Metrics API for HPA and kubectl top.

### 123. How do you check if metrics-server is running?
```bash
kubectl get deployment metrics-server -n kube-system
kubectl get pods -n kube-system | grep metrics-server
```

### 124. What is the difference between HPA v1 and v2?
- v1: CPU-based only
- v2: CPU, memory, custom, and external metrics

### 125. How do you check HPA status?
```bash
kubectl get hpa
kubectl describe hpa <hpa-name>
kubectl get hpa -w  # Watch for changes
```

### 126. What causes HPA to not scale?
- metrics-server not installed or running
- Resources not requested in Pod spec
- Insufficient nodes to scale out
- HPA misconfigured (wrong target ref or metrics)

**Troubleshooting:**
```bash
kubectl describe hpa <hpa-name>
kubectl get events -n <namespace>
kubectl logs -n kube-system -l k8s-app=metrics-server
```

### 127. How do you use custom metrics with HPA?
Deploy a custom metrics provider (Prometheus, Stackdriver) and reference metrics in HPA spec.

```yaml
metrics:
- type: Pods
    pods:
        metric:
            name: http_requests_per_second
        target:
            type: AverageValue
            averageValue: "1000"
```

## Vertical Pod Autoscaler (VPA)

### 128. What is a Vertical Pod Autoscaler?
VPA automatically adjusts CPU and memory requests/limits of Pods based on observed usage.

### 129. How do you create a VPA?
```yaml
apiVersion: autoscaling.k8s.io/v1
kind: VerticalPodAutoscaler
metadata:
    name: app-vpa
spec:
    targetRef:
        apiVersion: "apps/v1"
        kind: Deployment
        name: app-deployment
    updatePolicy:
        updateMode: "Auto"
    resourcePolicy:
        containerPolicies:
        - containerName: "*"
            minAllowed:
                cpu: 100m
                memory: 128Mi
            maxAllowed:
                cpu: 2
                memory: 2Gi
```

### 130. VPA update modes?
- `Off`: Only provides recommendations
- `Initial`: Recommendations applied at Pod creation
- `Recreate`: Updates running Pods by recreating them
- `Auto`: Uses best available update (Recreate or In-place)

### 131. Difference between HPA and VPA?
- HPA: Scales number of Pods based on metrics
- VPA: Adjusts resource requests/limits of existing Pods

### 132. Can HPA and VPA work together?
Not recommended; they can conflict. Use HPA for scale and set VPA in `Off` mode for recommendations only.

### 133. How do you check VPA recommendations?
```bash
kubectl describe vpa <vpa-name>
kubectl get vpa
```

## CoreDNS

### 134. What is CoreDNS?
CoreDNS is the DNS server for Kubernetes clusters, providing service discovery and DNS resolution for services.

### 135. How does CoreDNS work?
CoreDNS runs as a Deployment in kube-system namespace and is exposed via a ClusterIP Service. It resolves service names to IPs using pod IP addresses.

### 136. How do you check CoreDNS status?
```bash
kubectl get deployment coredns -n kube-system
kubectl get pods -n kube-system -l k8s-app=kube-dns
kubectl get service kube-dns -n kube-system
```

### 137. What is CoreDNS ConfigMap?
The ConfigMap in kube-system named `coredns` contains the CoreDNS configuration (Corefile).

```bash
kubectl get configmap coredns -n kube-system
kubectl edit configmap coredns -n kube-system
```

### 138. How does DNS resolution work in Kubernetes?
1. Pod queries CoreDNS ClusterIP
2. CoreDNS resolves service name to Endpoints
3. CoreDNS returns Pod IP(s)
4. Pod connects to service

### 139. What is service discovery in Kubernetes?
DNS-based service discovery: `<service-name>.<namespace>.svc.cluster.local`

Example: `nginx-service.default.svc.cluster.local`

### 140. How do you troubleshoot DNS issues?
```bash
# Check CoreDNS pods
kubectl get pods -n kube-system -l k8s-app=kube-dns

# Test DNS from pod
kubectl run -it --image=busybox dns-test -- sh
nslookup nginx-service
nslookup nginx-service.default

# Check logs
kubectl logs -n kube-system -l k8s-app=kube-dns
```

### 141. What causes DNS resolution failures?
- CoreDNS pod not running
- CoreDNS service misconfigured
- Network policies blocking DNS port 53
- Incorrect service name
- Service doesn't exist

### 142. How do you add custom DNS records to CoreDNS?
Edit the CoreDNS ConfigMap and add custom entries in the Corefile configuration.

## Metrics Server

### 143. What is Metrics Server?
Metrics Server collects resource metrics from Kubelets and provides them via Metrics API for HPA, VPA, and `kubectl top`.

### 144. How do you install Metrics Server?
```bash
kubectl apply -f https://github.com/kubernetes-sigs/metrics-server/releases/latest/download/components.yaml

# Or via Helm
helm install metrics-server metrics-server/metrics-server -n kube-system
```

### 145. How do you check Metrics Server status?
```bash
kubectl get deployment metrics-server -n kube-system
kubectl get pods -n kube-system -l k8s-app=metrics-server
kubectl logs -n kube-system -l k8s-app=metrics-server
```

### 146. How do you view resource usage?
```bash
kubectl top nodes
kubectl top pods
kubectl top pods -n <namespace>
kubectl top pods --all-namespaces
```

### 147. What causes `kubectl top` to fail?
- Metrics Server not installed
- Metrics not yet collected (wait 30-60 seconds after pod creation)
- Metrics Server pod not running
- Insufficient node resources

**Troubleshooting:**
```bash
kubectl describe pod <pod-name>
kubectl logs -n kube-system -l k8s-app=metrics-server
```

### 148. How do you check Metrics API availability?
```bash
kubectl get --raw /apis/metrics.k8s.io/v1beta1/nodes
```

### 149. What metrics does Metrics Server collect?
- CPU usage
- Memory usage
- Pod metrics
- Node metrics

## API Server

### 150. What is kube-apiserver?
The central API server that exposes the Kubernetes API; all requests go through it (create, read, update, delete resources).

### 151. What are kube-apiserver components?
- Authentication: Verify user identity
- Authorization: Check permissions
- Admission control: Validate/mutate requests
- Storage: etcd backend

### 152. How do you check API server status?
```bash
kubectl get pods -n kube-system -l component=kube-apiserver
kubectl logs -n kube-system -l component=kube-apiserver
```

### 153. What is API server port?
Default port is 6443 for secure API access (https).

### 154. How do you access API server directly?
```bash
kubectl proxy --port=8080
curl http://localhost:8080/api/v1/namespaces
```

### 155. What are API server admission controllers?
Plugins that intercept and validate/mutate requests before they're persisted.

Examples: PodSecurityPolicy, ResourceQuota, LimitRanger, ValidatingWebhook, MutatingWebhook.

### 156. How do you view API server audit logs?
Audit logging must be enabled on the API server; logs are written to configured backend.

```bash
kubectl logs -n kube-system -l component=kube-apiserver | grep audit
```

### 157. What causes API server to be unavailable?
- API server pod crashed or not running
- etcd connectivity issues
- Insufficient node resources
- Network issues

**Troubleshooting:**
```bash
kubectl get pods -n kube-system | grep apiserver
kubectl describe pod kube-apiserver-<node> -n kube-system
kubectl logs -n kube-system -l component=kube-apiserver
```

### 158. How do you check API server certificates?
```bash
kubectl get secret -n kube-system | grep apiserver
kubectl get secret apiserver-kubelet-client-cert -n kube-system
```

## Etcd

### 159. What is etcd?
etcd is a distributed key-value store that persists all Kubernetes cluster state including resources, configurations, and state.

### 160. Where does etcd store data?
Default location: `/var/lib/etcd/` on the control-plane node(s).

### 161. How do you check etcd status?
```bash
kubectl get pods -n kube-system -l component=etcd
kubectl logs -n kube-system -l component=etcd
```

### 162. How do you backup etcd?
```bash
# Using etcdctl
ETCDCTL_API=3 etcdctl --endpoints=https://127.0.0.1:2379 \
  --cacert=/etc/kubernetes/pki/etcd/ca.crt \
  --cert=/etc/kubernetes/pki/etcd/server.crt \
  --key=/etc/kubernetes/pki/etcd/server.key \
  snapshot save backup.db

# Or use kubectl
kubectl get all -A -o yaml > backup.yaml
```

### 163. How do you restore etcd?
```bash
ETCDCTL_API=3 etcdctl --endpoints=https://127.0.0.1:2379 \
  --cacert=/etc/kubernetes/pki/etcd/ca.crt \
  --cert=/etc/kubernetes/pki/etcd/server.crt \
  --key=/etc/kubernetes/pki/etcd/server.key \
  snapshot restore backup.db --data-dir=/var/lib/etcd-restored
```

### 164. What is etcd database size?
Check with: `du -sh /var/lib/etcd/`

Large etcd can cause slow cluster performance; defragmentation may help.

### 165. How do you defragment etcd?
```bash
ETCDCTL_API=3 etcdctl --endpoints=https://127.0.0.1:2379 \
  --cacert=/etc/kubernetes/pki/etcd/ca.crt \
  --cert=/etc/kubernetes/pki/etcd/server.crt \
  --key=/etc/kubernetes/pki/etcd/server.key \
  defrag
```

### 166. What causes etcd to be unavailable?
- etcd pod crashed or not running
- Disk space full
- Network partition
- Corrupted database
- Too many concurrent requests

**Troubleshooting:**
```bash
kubectl get pods -n kube-system | grep etcd
kubectl logs -n kube-system -l component=etcd
df -h /var/lib/etcd/
```

### 167. How do you check etcd cluster health?
```bash
ETCDCTL_API=3 etcdctl --endpoints=https://127.0.0.1:2379 \
  --cacert=/etc/kubernetes/pki/etcd/ca.crt \
  --cert=/etc/kubernetes/pki/etcd/server.crt \
  --key=/etc/kubernetes/pki/etcd/server.key \
  endpoint health
```

### 168. What is etcd quorum?
In a multi-node etcd cluster, quorum is required for writes. Formula: `(n/2) + 1` for n nodes.

3-node cluster requires 2 nodes healthy; 5-node requires 3 nodes.

### 169. What happens if etcd loses quorum?
Cluster becomes read-only; no new writes allowed until quorum is restored.

### 170. How do you recover etcd from backup?
Stop the API server and Kubelet, restore etcd data directory, then restart services.

