
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
