# Chapter 01 – CI/CD (Jenkins & GitHub Actions)

# Part 02 – GitHub Actions, Jenkins Pipeline Design

---

# Table of Contents

11. GitHub Actions Architecture
12. Jenkins Architecture
13. Pipeline Stages
14. Environment Variables
15. Secrets Management
16. YAML Workflow
17. Jenkinsfile
18. Branch Protection
19. Quality Gates
20. Pipeline Optimization

---

# Interview Question 11

## What is GitHub Actions?

### Short Interview Answer

GitHub Actions is GitHub's built-in Continuous Integration and Continuous Delivery (CI/CD) platform. It allows developers to automate building, testing, packaging, and deploying applications whenever events occur in a GitHub repository.

---

### Detailed Answer

GitHub Actions uses event-driven workflows.

When an event occurs, such as:

- Push
- Pull Request
- Release
- Schedule
- Manual Trigger

GitHub automatically starts a workflow defined in a YAML file.

The workflow consists of:

- Workflow
- Jobs
- Steps
- Actions
- Runner

Everything is stored alongside the application code.

---

### Architecture

```
Developer

↓

Git Push

↓

GitHub Repository

↓

Workflow Trigger

↓

GitHub Runner

↓

Checkout Code

↓

Build

↓

Test

↓

Package

↓

Deploy

↓

Reports
```

---

### Follow-up Questions

- Where are workflows stored?
- What is a Runner?
- Can GitHub Actions deploy applications?

---

### Best Practices

✔ Keep workflows modular

✔ Use reusable workflows

✔ Cache dependencies

✔ Store secrets securely

✔ Separate build and deployment

---

# Interview Question 12

## Explain GitHub Actions Workflow Structure.

### Short Interview Answer

A GitHub Actions workflow is a YAML file located under:

```
.github/workflows/
```

It defines:

- Trigger
- Jobs
- Steps
- Runner
- Environment
- Secrets

---

### Example

```yaml
name: QA Pipeline

on:
  push:
    branches:
      - main

jobs:

  build:

    runs-on: ubuntu-latest

    steps:

      - uses: actions/checkout@v4

      - uses: actions/setup-java@v4

      - run: mvn clean test
```

---

### Explanation

Workflow

↓

Jobs

↓

Steps

↓

Actions

↓

Commands

---

### Interview Tip

Remember:

One Workflow

↓

Many Jobs

↓

Many Steps

---

# Interview Question 13

## What is Jenkins?

### Short Interview Answer

Jenkins is an open-source automation server used to automate software builds, testing, and deployment through configurable pipelines.

---

### Detailed Answer

Jenkins is highly extensible using plugins.

It supports:

- Java
- .NET
- NodeJS
- Python
- Docker
- Kubernetes
- AWS
- Azure
- GitHub
- GitLab

Unlike GitHub Actions, Jenkins can be hosted completely on-premises.

---

### Jenkins Architecture

```
Developer

↓

Git

↓

Jenkins Master

↓

Agent 1

Agent 2

Agent 3

↓

Build

↓

Automation

↓

Deploy
```

---

### Master Responsibilities

- Schedule Jobs
- Manage Plugins
- Authentication
- Pipeline Coordination

---

### Agent Responsibilities

- Execute Builds
- Run Selenium Tests
- Build Docker Images
- Deploy Applications

---

# Interview Question 14

## What is the difference between Jenkins Master and Agent?

### Short Interview Answer

The Jenkins Master manages the pipeline, while Agents perform the actual work.

---

### Responsibilities

Master

- Scheduling
- Authentication
- Plugins
- Job Management

Agent

- Execute Jobs
- Compile Code
- Run Tests
- Build Images

---

### Why Use Multiple Agents?

Benefits

- Parallel execution
- Better performance
- Load balancing
- Different operating systems

Example

Windows Agent

↓

.NET Tests

Linux Agent

↓

Java Tests

Mac Agent

↓

iOS Tests

---

# Interview Question 15

## What are Pipeline Stages?

### Short Interview Answer

Pipeline stages divide the CI/CD workflow into logical sections such as Build, Test, Package, Deploy, and Report.

---

### Example

```
Checkout

↓

Compile

↓

Unit Tests

↓

API Tests

↓

UI Automation

↓

Performance Smoke

↓

Package

↓

Deploy QA

↓

Regression

↓

Deploy Production
```

---

### Why Use Stages?

- Better visibility
- Easier debugging
- Parallel execution
- Faster pipelines

---

### Best Practice

Each stage should have one clear responsibility.

---

# Interview Question 16

## What are Environment Variables?

### Short Interview Answer

Environment variables are configurable values used by pipelines to avoid hardcoding information such as URLs, usernames, and environment names.

---

### Examples

```
BASE_URL

USERNAME

PASSWORD

JAVA_HOME

NODE_VERSION

TEST_ENV

BROWSER
```

---

### GitHub Example

```yaml
env:

  TEST_ENV: QA

  BROWSER: Chrome
```

---

### Benefits

✔ Easy configuration

✔ Multiple environments

✔ No code changes

✔ Secure deployment

---

# Interview Question 17

## How are Secrets Managed in GitHub Actions?

### Short Interview Answer

Sensitive information such as passwords, API keys, and tokens should be stored as GitHub Secrets instead of hardcoding them in source code.

---

### Examples

- Database Password

- AWS Key

- Azure Credentials

- Docker Token

- API Key

---

### Example

```yaml
env:

  TOKEN: ${{ secrets.GITHUB_TOKEN }}
```

---

### Best Practices

✔ Never commit passwords

✔ Rotate secrets regularly

✔ Use least privilege

✔ Audit secret access

---

### Common Mistake

❌

```
password = admin123
```

✔

```
password = ${{ secrets.DB_PASSWORD }}
```

---

# Interview Question 18

## What is a Jenkinsfile?

### Short Interview Answer

A Jenkinsfile is a text file that defines the Jenkins pipeline using Groovy syntax. It allows pipeline configuration to be stored alongside the application source code.

---

### Example

```groovy
pipeline {

    agent any

    stages {

        stage('Build') {

            steps {

                sh 'mvn clean package'

            }

        }

        stage('Test') {

            steps {

                sh 'mvn test'

            }

        }

    }

}
```

---

### Benefits

✔ Version Controlled

✔ Repeatable

✔ Easy Maintenance

✔ Infrastructure as Code

---

# Interview Question 19

## What are Branch Protection Rules?

### Short Interview Answer

Branch Protection Rules prevent developers from making unsafe changes directly to important branches such as `main` or `master`.

---

### Typical Rules

✔ Pull Request Required

✔ Minimum Reviewers

✔ Status Checks Passed

✔ Build Success Required

✔ No Force Push

✔ No Direct Commits

---

# Interview Question 20

## What is a Quality Gate?

### Short Interview Answer

A Quality Gate is a checkpoint within the CI/CD pipeline that determines whether the software meets predefined quality standards before moving to the next stage.

---

### Common Quality Gates

✔ Unit Tests

✔ Automation Tests

✔ API Tests

✔ Code Coverage

✔ Static Code Analysis

✔ Security Scan

✔ Performance Smoke Test

---

### Enterprise Example

```
Developer Push

↓

Compile

↓

Unit Tests

↓

SonarQube

↓

API Tests

↓

UI Tests

↓

Performance Smoke

↓

Quality Gate

↓

Deploy QA
```

---

### Typical Quality Gate Rules

- Build must succeed
- No Critical Vulnerabilities
- Code Coverage > 80%
- Smoke Tests = 100% Pass
- No High Severity Defects
- Sonar Quality Gate = Passed

---

### Best Practices

✔ Fail Fast

✔ Small Pipelines

✔ Automated Decisions

✔ Actionable Reports

✔ Fast Feedback

---

# Interview Cheat Sheet

## GitHub Actions

- YAML-based
- Event Driven
- GitHub Integrated
- Marketplace Actions
- Cloud + Self-hosted Runners

---

## Jenkins

- Plugin Based
- Groovy Pipelines
- Master-Agent Architecture
- Self Hosted
- Highly Customizable

---

## Secrets

Never hardcode:

- Passwords
- Tokens
- Certificates
- API Keys

Always use:

- GitHub Secrets
- Jenkins Credentials
- Azure Key Vault
- AWS Secrets Manager

---

## Enterprise Pipeline Flow

```
Developer

↓

Commit

↓

Pull Request

↓

Build

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

Deploy QA

↓

Regression

↓

Manual Approval

↓

Deploy Production
```

---

# Quick Revision

Remember these interview keywords:

- Workflow
- Runner
- Pipeline
- Stage
- Job
- Step
- Artifact
- Trigger
- Environment Variables
- Secrets
- Jenkinsfile
- YAML
- Branch Protection
- Quality Gate
- Master-Agent
- Parallel Execution
