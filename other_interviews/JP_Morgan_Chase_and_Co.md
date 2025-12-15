# JP Morgan Chase & Co – Cloud / DevOps Interview Questions & Answers

This document contains **real-world AWS, ECS, EC2, networking, scaling, security, and production design questions** with **practical, interview-oriented answers**.

---

## 1. How can you scale the server in AWS Cloud?

AWS provides two types of scaling:

### Vertical Scaling
- Increase instance size (t2.micro → t3.large)
- Requires restart
- Limited and not ideal for production

### Horizontal Scaling (Recommended)
- Use **Auto Scaling Group (ASG)**
- Add/remove EC2 instances based on:
  - CPU
  - Memory (via CloudWatch agent)
  - Request count

Usually combined with **Load Balancer** for traffic distribution.

---

## 2. What is an AWS global outage?

An AWS global outage occurs when **multiple AWS regions or global services** (like Route 53, IAM, CloudFront) experience failures simultaneously.

Examples:
- Route 53 DNS failure
- IAM authentication outage
- S3 global service disruption

Impact:
- Applications across regions may be affected
- Region-specific outages are more common than true global outages

---

## 3. Design an infrastructure so that if a global outage occurs, we can switch to another region.

### Multi-Region Architecture
- Deploy application in **two or more regions**
- Use **Route 53 routing policies**:
  - Failover routing
  - Latency-based routing
- Replicate data using:
  - S3 Cross-Region Replication
  - RDS Read Replicas / Global Database
- Keep infra defined via **Terraform**

Failover can be:
- **Automatic** (health checks)
- **Manual** (DNS switch)

---

## 4. Have you worked on ECS? Explain it.

Yes. **Amazon ECS (Elastic Container Service)** is a managed container orchestration service.

Key components:
- Cluster
- Task Definition
- Service
- Task
- Launch types:
  - EC2
  - Fargate (serverless)

Benefits:
- No control-plane management
- Integrated with ALB, IAM, CloudWatch
- Easy scaling and deployment

---

## 5. What is a private subnet?

A **private subnet**:
- Has no direct internet access
- Does not route traffic to Internet Gateway
- Uses **NAT Gateway** for outbound internet access

Used for:
- EC2
- ECS tasks
- Databases

---

## 6. In which subnet is your server placed?

- **Application servers** → Private Subnet
- **Load Balancers** → Public Subnet
- **Databases** → Private Subnet

This follows AWS security best practices.

---

## 7. How do you expose your private server to the application?

Using:
- **Application Load Balancer (ALB)** or **Network Load Balancer (NLB)**
- Load balancer is public
- Targets (EC2/ECS) are private

Traffic flow:
User → Load Balancer → Private Server

---

## 8. Why are you using Network Load Balancer in your project?

We use **NLB** because:
- Handles **TCP / TLS traffic**
- Very high performance & low latency
- Preserves client IP
- Suitable for microservices, gRPC, WebSockets

ALB is used for HTTP/HTTPS, while NLB is preferred for **network-level traffic**.

---

## 9. How do you enable Auto Scaling Group so load is distributed?

Steps:
1. Create Launch Template
2. Create Auto Scaling Group
3. Attach ASG to Load Balancer
4. Define scaling policies:
   - Target tracking (CPU 60%)
   - Step scaling
5. Monitor using CloudWatch

This ensures:
- High availability
- Automatic scaling during peak load

---

## 10. In ECS, if a running task faces a timeout issue, how do you resolve it?

Steps to troubleshoot:
- Check ALB idle timeout
- Check container timeout configuration
- Increase ECS task CPU/memory
- Check application-level timeouts
- Review CloudWatch logs

Often timeouts occur due to:
- Insufficient resources
- Load balancer timeout mismatch

---

## 11. In CloudTrail, if someone changed a service, how do you verify who did it?

Steps:
1. Open CloudTrail
2. Search event name (e.g., `ModifyInstanceAttribute`)
3. Check:
   - `userIdentity`
   - IAM role or user
   - Source IP
   - Time of change

CloudTrail provides **full audit history**.

---

## 12. S3 upload triggers Lambda, but today it didn’t trigger – why?

Possible reasons:
- Event notification deleted or misconfigured
- Lambda permission missing (`InvokeFunction`)
- Upload happened in different prefix
- Object overwritten (PUT vs COPY)
- Lambda concurrency limit exceeded

Check:
- S3 event configuration
- Lambda logs in CloudWatch

---

## 13. If EC2 faces load in the future, how do you prepare today?

Best practices:
- Use Auto Scaling Group
- Use Load Balancer
- Enable CloudWatch alarms
- Use stateless architecture
- Store state in external DB/cache

This ensures **future scalability without downtime**.

---

## 14. How do you deploy 6 microservices on EC2 using one ALB?

Use **ALB path-based routing**:
- `/service1` → Target Group 1
- `/service2` → Target Group 2
- `/service3` → Target Group 3

Each microservice:
- Separate EC2 instances or containers
- Separate target groups

---

## 15. How do you expose an app in a private subnet?

Options:
- Public ALB → Private EC2/ECS
- API Gateway + VPC Link
- Bastion Host (admin access only)

Never expose private instances directly.

---

## 16. Java 21 deployed on server – what configurations are required?

Server configuration:
- Install Java 21 (Amazon Corretto / OpenJDK)
- Set `JAVA_HOME`
- Update `PATH`
- Increase heap size:
  - `-Xms`, `-Xmx`
- OS tuning:
  - File descriptors
  - Memory limits

Also ensure compatibility with application dependencies.

---

## 17. If someone changed an IAM role, how do you modify or track it?

Tracking:
- Use CloudTrail to identify change
- Review policy version history

Modification:
- Update role via IAM console or IaC
- Prefer Terraform for controlled changes
- Enable approval & review process

---

## 📌 Final Notes
- Always design for **high availability**
- Use **private subnets + load balancers**
- Automate infra using **Terraform**
- Monitor and audit using **CloudWatch & CloudTrail**

---

### ⭐ Author
Cloud / DevOps Engineer  
Focused on AWS, ECS, EC2, Load Balancing, Security, and Scalable Architectures
