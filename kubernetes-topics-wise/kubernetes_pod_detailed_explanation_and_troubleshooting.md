Kubernetes Pod – Detailed Explanation, Causes & Troubleshooting Guide

This document provides a deep, practical explanation of Kubernetes Pods, covering:

What a Pod is

Why Pods exist

Pod lifecycle

Common failure causes

Step-by-step troubleshooting

Interview-ready explanations

1. What is a Pod in Kubernetes?

A Pod is the smallest deployable unit in Kubernetes.
It represents one or more containers that:

Share the same network namespace (same IP address)

Share storage volumes

Are scheduled together on the same node

Important point:
Kubernetes does not deploy containers directly — it always deploys Pods.

2. Why Pods Exist (Design Reason)
Cause

Containers alone do not provide:

Scheduling

Coordinated networking

Shared storage

Lifecycle management

Solution

A Pod acts as a wrapper around containers and provides:

One IP address

Shared volumes

A single lifecycle unit

3. Single-Container vs Multi-Container Pod
Single-Container Pod (Most Common)

One application per Pod

Easier scaling

Easier troubleshooting

Multi-Container Pod (Sidecar Pattern)

Used when containers are tightly coupled, such as:

Application + log shipper

Application + proxy

Application + config reloader

4. Pod Lifecycle (Very Important for Interviews)

Pod lifecycle flow:

Pending → Running → Succeeded / Failed
Repeated failures lead to CrashLoopBackOff

State explanations:

Pending: Pod is created but not scheduled or image not pulled

Running: Containers are running

Succeeded: Job finished successfully

Failed: Container exited with error

CrashLoopBackOff: Container keeps crashing and restarting

5. Common Pod Failure Causes & Overview

Most Pod issues happen due to:

Resource constraints

Image issues

Configuration or secret problems

Application crashes

Node-level problems

Fastest debugging approach:

Describe the Pod

Check Events

Check Logs

6. Pod Stuck in Pending State
Common Causes

Insufficient CPU or memory on nodes

No available nodes

Node selector or affinity mismatch

PersistentVolumeClaim not bound

Node taints without tolerations

What to Check

Events section in pod description

Resource requests

Node availability

PVC status

Resolution

Add more nodes or increase node size

Reduce CPU/memory requests

Fix node selectors or affinity rules

Bind PVC or create proper StorageClass

7. Pod in ImagePullBackOff or ErrImagePull
Causes

Wrong image name or tag

Image not pushed to registry

Authentication failure (ECR / Docker Hub)

Network issue

Troubleshooting

Check pod events

Verify image name and tag

Validate image pull secrets

Verify IAM role permissions (for ECR)

Resolution

Fix image name or tag

Push image to registry

Configure registry credentials correctly

8. Pod in CrashLoopBackOff
Common Causes

Application crashes on startup

Missing environment variables

Incorrect ConfigMap or Secret

Memory limit too low (OOMKilled)

Application exits immediately

Troubleshooting

Check current pod logs

Check previous container logs

Review exit codes

Verify configs and secrets

Resolution

Fix application startup issues

Correct ConfigMaps and Secrets

Increase memory limits

Improve application error handling

9. Pod Running but Application Not Accessible
Causes

Wrong containerPort

Service selector mismatch

Readiness probe failing

NetworkPolicy blocking traffic

Troubleshooting

Verify Service configuration

Check Endpoints

Inspect readiness probe status

Validate labels and selectors

Resolution

Fix labels and selectors

Correct port mappings

Adjust readiness probe

Update NetworkPolicy rules

10. Pod OOMKilled (Out of Memory)
Causes

Memory limit too low

Memory leak in application

Runtime (JVM/Node) misconfiguration

Identification

Pod description shows:
Reason: OOMKilled

Resolution

Increase memory limits

Optimize application memory usage

Add monitoring and alerts

11. Pod Evicted
Causes

Node memory pressure

Disk pressure

CPU pressure

Node resource exhaustion

Troubleshooting

Check eviction reason in pod events

Review node conditions

Resolution

Increase node capacity

Add more nodes

Tune resource requests and limits

12. Pod Restarting Frequently
Causes

Liveness probe failures

Aggressive probe settings

Unstable application behavior

Troubleshooting

Check restart count

Review liveness probe configuration

Resolution

Increase initial delay

Adjust probe intervals

Fix application health endpoint

13. Pod Not Scheduled on Expected Node
Causes

Node taints without tolerations

Node affinity or anti-affinity rules

NodeSelector mismatch

Troubleshooting

Review scheduling events

Check node labels and taints

Resolution

Add tolerations

Fix affinity rules

Correct node labels

14. Best Practices for Pod Stability

Always define CPU and memory requests and limits

Use readiness and liveness probes

Externalize configuration using ConfigMaps and Secrets

Avoid running containers as root

Monitor pod metrics continuously

15. Pod vs Container (Interview Question)

Pod:

Kubernetes abstraction

Has its own IP

Can run multiple containers

Container:

Runtime process

No independent IP

Runs inside a Pod

16. Pod Troubleshooting Checklist

Check pod status

Describe the pod

Check logs

Check previous logs

Review Events

Verify configs, secrets, and resources

17. Interview-Ready One-Liner

A Pod is the smallest deployable unit in Kubernetes that encapsulates one or more containers sharing networking and storage. Most Pod issues are caused by configuration errors, resource limits, or application crashes and can be diagnosed using pod events and logs.

18. Summary

Pods are ephemeral

Kubernetes continuously reconciles desired state

Pod failures are predictable and observable

Strong Pod design leads to stable production workloads

Author

Velanati Naveen Kumar
DevOps Engineer
CI/CD | AWS | Kubernetes | Terraform | GitOps | Automation
+91 9848545101

If you want, I can next provide:

CrashLoopBackOff-only deep dive

EKS-specific Pod issues

Pod YAML best practices

Interview rapid-fire Q&A

Just say the word 👍
