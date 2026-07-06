## Part 01 – Test Strategy Fundamentals

---

# Table of Contents

1. What is Test Strategy?
2. Test Strategy vs Test Plan
3. Components of a Test Strategy
4. Risk-Based Testing
5. Entry Criteria
6. Exit Criteria
7. Test Deliverables
8. Requirement Traceability Matrix (RTM)
9. Test Estimation
10. Test Environment Planning
11. Interview Questions (Q1–Q15)

---

# Why Test Strategy Matters

Many engineers know **how to automate tests**.

Senior QA Engineers know **what should be tested, why it should be tested, and when it should be tested**.

A Test Strategy answers these questions before testing begins.

---

# What is a Test Strategy?

## Definition

A Test Strategy is a high-level document that defines the overall approach, objectives, scope, testing types, tools, environments, risks, and success criteria for a project.

It answers:

- What are we testing?
- Why are we testing it?
- How will we test it?
- Who will test it?
- When will testing occur?
- What defines success?

---

# Characteristics of a Good Test Strategy

A good strategy should be:

- Clear
- Practical
- Risk-focused
- Measurable
- Reusable
- Flexible
- Aligned with business goals

---

# Typical Test Strategy

```text
Requirements

↓

Test Strategy

↓

Test Planning

↓

Test Design

↓

Execution

↓

Reporting

↓

Release Decision
```

---

# Test Strategy vs Test Plan

Many interviewers ask this question.

| Test Strategy | Test Plan |
|---------------|-----------|
| High-level approach | Project-specific execution plan |
| Defines "how" testing will be performed | Defines "when", "who", and "what" |
| Usually created once | Created for each project or release |
| Long-term | Short-term |
| Focuses on overall testing direction | Focuses on execution details |

---

## Simple Way to Remember

**Strategy = Vision**

**Plan = Execution**

---

# Components of a Test Strategy

A typical strategy includes:

- Scope
- Objectives
- Test Levels
- Test Types
- Automation Strategy
- Test Environment
- Test Data Strategy
- Defect Management
- Entry Criteria
- Exit Criteria
- Risks
- Reporting
- Metrics

---

# Risk-Based Testing

## Definition

Risk-Based Testing prioritizes testing based on business impact and the likelihood of failure.

Instead of testing everything equally, focus on the areas with the highest risk.

---

# Risk Matrix

| Business Impact | Probability | Priority |
|-----------------|-------------|----------|
| High | High | Critical |
| High | Low | High |
| Low | High | Medium |
| Low | Low | Low |

---

## Example

E-commerce Website

High Priority

- Login
- Payment
- Checkout
- Order Placement

Lower Priority

- Theme Settings
- Profile Picture
- Help Page

---

## Interview Tip

If you have limited time before a release, always explain that you would prioritize high-risk and business-critical functionality first.

---

# Entry Criteria

## Definition

Entry Criteria define the conditions that must be met before testing begins.

Examples:

- Requirements approved
- Build deployed
- Test environment available
- Test data prepared
- Test cases reviewed

---

# Exit Criteria

## Definition

Exit Criteria define the conditions that must be be satisfied before testing can be completed.

Examples:

- No Critical defects
- No High severity open defects
- Regression completed
- Smoke tests passed
- Test reports completed
- Business approval received

---

# Test Deliverables

Typical QA deliverables include:

- Test Strategy
- Test Plan
- Test Cases
- Automation Scripts
- Test Data
- Defect Reports
- Test Execution Report
- Release Recommendation

---

# Requirement Traceability Matrix (RTM)

## Definition

An RTM ensures every requirement is covered by one or more test cases.

Example

| Requirement | Test Case | Status |
|-------------|-----------|--------|
| Login | TC-001 | Passed |
| Password Reset | TC-002 | Passed |
| Payment | TC-003 | Failed |

---

## Why RTM?

Benefits:

- Complete test coverage
- Easier impact analysis
- Audit support
- Missing requirement detection

---

# Test Estimation

## Common Estimation Factors

Consider:

- Number of requirements
- Complexity
- Automation availability
- Team size
- Dependencies
- Risks
- Environment readiness

---

## Estimation Example

Suppose a release contains:

- 40 new requirements
- 200 regression tests
- 10 APIs
- 5 UI workflows

Estimate effort separately for:

- Test design
- Automation updates
- Execution
- Regression
- Defect verification

---

# Test Environment Planning

Questions to ask:

- Which environment?
- Which database?
- Which API endpoints?
- Which browser versions?
- Which user accounts?
- Which external integrations?

---

# Environment Checklist

✔ Stable build

✔ Correct configuration

✔ Test accounts

✔ Test data

✔ Third-party services available

✔ Monitoring enabled

---

# Interview Questions

---

# Q1. What is a Test Strategy?

## Short Interview Answer

A Test Strategy is a high-level document that defines the overall testing approach, objectives, scope, tools, environments, risks, and success criteria for a project.

---

## Senior Interview Answer

> A Test Strategy defines how quality will be achieved across the project. It aligns testing activities with business objectives, identifies risks, selects appropriate testing techniques, and establishes measurable entry and exit criteria. It also guides automation, environments, reporting, and release decisions.

---

## Real Project Example

For a government application handling citizen services, I would prioritize authentication, authorization, and data integrity as high-risk areas. The strategy would include API, UI, regression, security, accessibility, and performance testing, with automation integrated into the CI/CD pipeline.

---

# Q2. What is the difference between a Test Strategy and a Test Plan?

## Strong Interview Answer

A Test Strategy defines the overall approach to testing and is generally stable across projects. A Test Plan is specific to a release or project and details the schedule, resources, scope, and execution activities.

---

# Q3. What is Risk-Based Testing?

## Strong Interview Answer

Risk-Based Testing prioritizes testing effort based on business impact and the likelihood of failure. Critical business functions such as login, payments, and order processing receive more testing than low-risk features.

---

# Q4. What are Entry Criteria?

Entry Criteria are the conditions that must be satisfied before testing begins, such as approved requirements, a deployed build, and an available test environment.

---

# Q5. What are Exit Criteria?

Exit Criteria define when testing can stop. Typical examples include completion of regression testing, no open critical defects, acceptable test coverage, and stakeholder approval.

---

# Q6. Why is an RTM important?

The Requirement Traceability Matrix ensures every requirement is covered by test cases and helps identify missing coverage during audits or change requests.

---

# Q7. How do you estimate testing effort?

## Strong Interview Answer

I estimate effort based on the number and complexity of requirements, testing scope, automation availability, dependencies, environment readiness, team experience, and project risks. I also include time for defect verification, regression testing, and contingency for unexpected issues.

---

# Q8. How do you prioritize testing when time is limited?

## Strong Interview Answer

I use a risk-based approach. I test business-critical and high-risk functionality first, followed by integration points, recently changed areas, and regression for impacted features. Lower-risk features are tested only if time permits.

---

# Q9. What should every Test Strategy include?

- Scope
- Objectives
- Risks
- Test Types
- Automation Strategy
- Environments
- Entry Criteria
- Exit Criteria
- Metrics
- Reporting

---

# Q10. What would you include in a release readiness recommendation?

I would summarize:

- Test execution results
- Open defects by severity
- Regression status
- Automation results
- Risks
- Environment status
- Overall quality assessment
- Go/No-Go recommendation

---

# Architect's Notes

## Problem

Every feature receives the same amount of testing.

↓

Testing takes too long.

Critical defects may still escape.

---

## Better Approach

```text
Business Requirements

↓

Risk Assessment

↓

High Risk

↓

More Testing

↓

Medium Risk

↓

Moderate Testing

↓

Low Risk

↓

Basic Validation
```

This ensures testing effort is aligned with business value rather than treating every feature equally.

# Q11. If you only have two days before release, how would you decide what to test?
## A strong answer is:

- Assess the changes in the release.
- Perform impact analysis.
- Prioritize high-risk and business-critical functionality.
- Execute smoke tests first.
- Run targeted regression on impacted areas.
- Validate APIs before UI where possible.
- Review open defects and their severity.
- Communicate residual risks before giving a Go/No-Go recommendation.

This demonstrates strategic thinking rather than simply listing testing types, which is exactly what senior interviewers look for.

---

# Quick Revision

Remember these concepts:

- Test Strategy
- Test Plan
- Risk-Based Testing
- Entry Criteria
- Exit Criteria
- RTM
- Test Deliverables
- Test Estimation
- Test Environment
- Release Readiness
- Go/No-Go Decision
- Business Risk
- Test Coverage
