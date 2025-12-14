
# CI/CD Pipelines - Jenkins Interview Questions

## Jenkins Security

**Q: How do you secure Jenkins credentials?**
A: Use Jenkins Credentials Store to encrypt and manage sensitive data (API keys, passwords). Store credentials in a separate credentials domain and restrict access using Role-Based Access Control (RBAC). Consider using HashiCorp Vault for external secret management.

**Q: What is the difference between declarative and scripted pipelines regarding security?**
A: Declarative pipelines provide a structured, sandboxed syntax with built-in safety checks. Scripted pipelines offer more flexibility but require careful handling of sensitive operations. Both support credential masking in logs.

## Jenkins Metrics & Monitoring

**Q: What metrics should you monitor in a Jenkins pipeline?**
A: Build duration, success/failure rates, queue time, resource utilization (CPU, memory), test coverage, deployment frequency, and lead time for changes.

**Q: How do you integrate Jenkins with monitoring tools?**
A: Use plugins like Prometheus, Grafana, or CloudWatch integrations to export metrics. Enable Jenkins metrics endpoint and configure dashboards to track pipeline health.

## Automation & Best Practices

**Q: How do you implement Infrastructure as Code (IaC) in CI/CD?**
A: Use tools like Terraform or CloudFormation in pipeline stages. Store IaC files in version control and validate syntax before deployment.

**Q: What is the purpose of automated testing in pipelines?**
A: Catch bugs early, ensure code quality, validate functionality before production deployment, and reduce manual testing overhead.

## Failure Handling

**Q: How do you handle pipeline failures?**
A: Implement retry logic, conditional stages, notifications (email/Slack), detailed logging, and rollback mechanisms. Use post-actions (always, failure, success) for cleanup and alerts.

**Q: What is a canary deployment and why is it important?**
A: Deploy new code to a small subset of users first to detect issues before full rollout. Reduces risk and allows quick rollback if problems occur.

**Q: How do you manage Jenkins plugins?**
A: Use the Jenkins Plugin Manager UI or Jenkins Configuration as Code (JCaC) to define plugins declaratively. Store plugin lists in version control, regularly update plugins, and test updates in a staging environment. Consider using Jenkins Update Center for centralized management and dependency resolution.


## Common CI/CD Troubleshooting Scenarios

**Q: How do you troubleshoot pipeline timeout issues?**
A: Identify bottlenecks using build logs and metrics. Increase timeout thresholds, optimize slow stages (parallel execution, caching), reduce test suite scope, or allocate more resources to agents.

**Q: What causes pipeline credential failures and how do you resolve them?**
A: Expired credentials, incorrect domain scoping, or permission issues. Verify credentials exist in Jenkins Credentials Store, check RBAC permissions, rotate expired credentials, and test credential access in a isolated job.

**Q: How do you debug failed deployments in production?**
A: Review deployment logs for errors, check resource availability, verify environment variables, validate IAM/permissions, and use canary deployments to catch issues early. Maintain detailed audit trails for post-mortem analysis.

**Q: What should you do if a Jenkins agent goes offline?**
A: Check agent connectivity and network issues, verify SSH/JNLP configurations, review agent logs, restart the agent, and ensure sufficient disk space. Configure agent reconnection settings and health monitoring.

**Q: How do you handle flaky tests in pipelines?**
A: Implement retry mechanisms for transient failures, isolate flaky tests to a separate stage, increase test timeouts, fix race conditions, and use test parallelization carefully. Monitor test stability metrics.
