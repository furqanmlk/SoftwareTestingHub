## Part 04 – Enterprise CI/CD Architecture, Deployment Strategies & Troubleshooting

---

# Table of Contents

31. Blue-Green Deployment
32. Canary Deployment
33. Rolling Deployment
34. Rollback Strategy
35. Docker Integration
36. Kubernetes Integration
37. Infrastructure as Code (IaC)
38. Pipeline Failure Troubleshooting
39. Flaky Tests in CI/CD
40. Senior Scenario Questions

---

# Q31. What is Blue-Green Deployment?

## Short Interview Answer

Blue-Green Deployment is a deployment strategy where two identical production environments are maintained. One environment serves live traffic while the other receives the new application version. After validation, traffic is switched to the new environment.

---

## Architecture

```text
                    Users
                      │
               Load Balancer
                /           \
               ▼             ▼
        Blue Environment   Green Environment
          Version 1         Version 2
             Live          Deployment & Testing

After validation:

Users
   │
   ▼
Load Balancer
   │
   ▼
Green Environment (Live)

Blue Environment becomes standby.
```

---

## Advantages

- Zero downtime deployment
- Easy rollback
- Production validation before release
- Reduced deployment risk

---

## Disadvantages

- Double infrastructure cost
- More operational complexity

---

## Interview Tip

Blue-Green deployment is commonly used in enterprise systems where downtime is unacceptable.

---

# Q32. What is Canary Deployment?

## Short Interview Answer

Canary Deployment gradually releases a new application version to a small percentage of users before rolling it out to everyone.

---

## Example

```text
100% Users

↓

Deploy Version 2 to 5%

↓

Monitor

↓

25%

↓

50%

↓

100%
```

---

## Benefits

- Lower production risk
- Easy monitoring
- Early issue detection
- Minimal customer impact

---

## Real Example

A payment service may expose Version 2 to only 5% of users. If no increase in errors or latency is observed, deployment continues until all users receive the new version.

---

# Q33. What is Rolling Deployment?

## Short Interview Answer

Rolling Deployment replaces application instances one at a time instead of replacing the entire environment.

---

## Architecture

```text
Server 1 → Update

Server 2 → Update

Server 3 → Update

Server 4 → Update
```

Users continue using healthy servers while updates are applied incrementally.

---

## Advantages

- No downtime
- Lower infrastructure cost than Blue-Green
- Gradual rollout

---

## Disadvantages

- Multiple application versions may run simultaneously
- Rollback is slower than Blue-Green

---

# Q34. How do you perform a Rollback?

## Short Interview Answer

Rollback restores the previous stable version when deployment validation fails.

---

## Rollback Workflow

```text
Deploy Version 2

↓

Smoke Tests

↓

Monitoring

↓

Failure Detected

↓

Rollback

↓

Deploy Version 1
```

---

## Rollback Triggers

- Smoke test failures
- Critical production errors
- Performance degradation
- High error rates
- Security issues

---

## Best Practices

- Keep previous artifacts
- Automate rollback
- Monitor application health
- Validate rollback success

---

# Q35. How does Docker fit into CI/CD?

## Short Interview Answer

Docker packages applications and their dependencies into containers, ensuring the same software runs consistently across development, testing, and production environments.

---

## CI/CD Flow

```text
Checkout

↓

Compile

↓

Run Tests

↓

Build Docker Image

↓

Push Image to Registry

↓

Deploy Container
```

---

## Example Commands

```bash
docker build -t qa-app:1.0 .

docker push qa-app:1.0
```

---

## Benefits

- Consistent environments
- Faster deployments
- Easy scaling
- Simplified dependency management

---

# Q36. How does Kubernetes integrate with CI/CD?

## Short Interview Answer

Kubernetes orchestrates containerized applications by automating deployment, scaling, load balancing, and self-healing.

---

## Pipeline

```text
Developer

↓

GitHub Actions

↓

Docker Image

↓

Container Registry

↓

Kubernetes Cluster

↓

Pods

↓

Users
```

---

## Kubernetes Features

- Auto Scaling
- Self Healing
- Rolling Updates
- Service Discovery
- Load Balancing

---

## Interview Tip

Docker creates containers.

Kubernetes manages containers.

---

# Q37. What is Infrastructure as Code (IaC)?

## Short Interview Answer

Infrastructure as Code is the practice of managing infrastructure using code instead of manual configuration.

---

## Common Tools

| Tool | Purpose |
|------|---------|
| Terraform | Cloud Infrastructure |
| ARM Templates | Azure Resources |
| CloudFormation | AWS Resources |
| Ansible | Configuration Management |

---

## Benefits

- Repeatable deployments
- Version control
- Automation
- Reduced configuration drift

---

## Example

Instead of manually creating servers, Terraform creates the environment automatically.

---

# Q38. How do you troubleshoot a failed CI/CD pipeline?

## Short Interview Answer

Troubleshooting begins by identifying the stage where the failure occurred and then analyzing logs, environment configuration, dependencies, and recent code changes.

---

## Troubleshooting Process

```text
Pipeline Failed

↓

Identify Failed Stage

↓

Review Logs

↓

Verify Environment

↓

Check Dependencies

↓

Reproduce Locally

↓

Fix

↓

Re-run Pipeline
```

---

## Common Causes

- Build failure
- Missing dependency
- Expired secrets
- Environment issue
- Test failure
- Network timeout
- Insufficient permissions

---

## Interview Tip

Always explain your troubleshooting process step by step instead of jumping to conclusions.

---

# Q39. How do you handle flaky tests in CI/CD?

## Short Interview Answer

Flaky tests produce inconsistent results without code changes. They should be identified, stabilized, and isolated to maintain pipeline reliability.

---

## Common Causes

- Timing issues
- Dynamic UI elements
- Hard-coded waits
- Test data dependency
- Shared environments
- Network latency

---

## Best Practices

- Replace Thread.sleep() with explicit waits
- Use stable locators
- Retry only transient failures
- Isolate flaky tests
- Review execution logs

---

## Real Example

A Selenium test failed intermittently due to asynchronous page loading. Replacing fixed waits with explicit waits and improving element synchronization eliminated the instability.

---

# Q40. Senior Interview Scenario

## Question

Your GitHub Actions pipeline suddenly increases from 15 minutes to 50 minutes. Developers are complaining that pull requests are taking too long.

How would you investigate and resolve the issue?

---

## Strong Interview Answer

> I would begin by reviewing the workflow execution history to determine which stage experienced the increase. I'd compare recent runs with previous successful executions and examine build logs for dependency downloads, infrastructure delays, or test failures. Next, I'd verify whether dependency caching is working correctly, confirm that runners are not overloaded, and identify whether new regression tests were introduced. If UI tests are consuming the majority of execution time, I'd separate smoke and regression suites, execute independent jobs in parallel, and leverage matrix builds where appropriate. I'd also investigate flaky tests that trigger unnecessary retries. Finally, I'd monitor the optimized pipeline to ensure execution time returns to an acceptable level while maintaining quality.

---

# Whiteboard Question

## Design an Enterprise CI/CD Pipeline

Expected discussion:

```text
Developer

↓

GitHub

↓

Pull Request

↓

Branch Protection

↓

GitHub Actions

↓

Checkout

↓

Dependency Cache

↓

Compile

↓

Unit Tests

↓

Static Analysis

↓

API Tests

↓

UI Automation

↓

Performance Smoke

↓

Security Scan

↓

Quality Gate

↓

Package Artifact

↓

Deploy DEV

↓

Deploy QA

↓

Regression

↓

UAT

↓

Manual Approval

↓

Deploy Production

↓

Monitoring

↓

Automatic Rollback
```

---

# Common Senior Interview Questions

- Explain Blue-Green Deployment.
- Explain Canary Deployment.
- Explain Rolling Deployment.
- How do you perform a rollback?
- Docker vs Kubernetes?
- What is Infrastructure as Code?
- How would you troubleshoot a failing pipeline?
- How do you reduce pipeline execution time?
- How do you manage flaky tests?
- What deployment strategy would you recommend for a banking application?

---

# Quick Revision

Remember these keywords:

- Blue-Green Deployment
- Canary Deployment
- Rolling Deployment
- Rollback
- Docker
- Kubernetes
- Infrastructure as Code
- Terraform
- Pipeline Troubleshooting
- Flaky Tests
- Monitoring
- Dependency Cache
- Matrix Builds
- Parallel Execution
- Quality Gates
