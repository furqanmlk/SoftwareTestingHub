# Technical Profile — Furqan Malik

---

## 1. Test Automation — Deep Dive

### Playwright + Python Framework (McAfee, 2020–Present)

> 🏆 Architected a unified Playwright + Python framework achieving 99% reliability in CI/CD quality gates across high-velocity release cycles.

**Coverage across all 3 JD-required layers:**
- **API layer** — RESTful microservice validation, response contract enforcement, data integrity checks
- **UI layer** — Playwright-driven browser automation for consumer-facing download and delivery flows
- **Integration layer** — end-to-end flows across backend security microservices and CDN delivery

**Framework design:**
- Modular fixtures, shared data factories, parallel execution with Dockerized isolation
- Test code reviewed in PRs, versioned in Git, maintained like application code — not throwaway scripts
- TypeScript variant also built for teams preferring typed test authoring

### Historical Automation Stack (2009–2020)

| Period | Stack | Highlight |
|---|---|---|
| BlackBerry 2009–2013 | Selenium + Python | Early Agile automation; Django-based test management app |
| McAfee 2014–2018 | C# + Python | 5,000+ suites at 95%+ coverage; UI, API, and load layers |
| Broadcom 2018–2019 | WebDriverIO + Selenium | Centralized reporting for global squads; 40% throughput increase |
| Equitable Life 2019 | Cypress + CI/CD | 40% regression cycle reduction |

---

## 2. CI/CD & Pipeline Engineering

### What You've Built

| Tool | Role |
|---|---|
| **GitHub Actions** | Lightweight pipelines for microservice smoke and contract tests |
| **Docker** | Containerized Linux test execution — reproducible, isolated, parallel |
| **Grafana** | Real-time pipeline health, pass/fail trends, flakiness rates by suite |

### Flakiness Strategy

> Flaky tests destroy team trust in automation. The approach below is proactive, not reactive.

- Statistical pass thresholds — tests must pass X% over rolling window before being trusted
- LLM-powered failure clustering — AI distinguishes real regressions from environment noise
- Self-healing scripts — auto-retry and quarantine flaky tests by pattern confidence score
- Anomaly detection — flags non-deterministic behavior in data-intensive services before production
- **Outcome:** pipeline failures get acted on because the signal-to-noise ratio is high

### Full Infrastructure Stack
`Jenkins` `GitHub Actions` `Docker` `Kubernetes` `AWS (ECR, CloudWatch)` `GCP` `Splunk` `ELK Stack` `Grafana` `Linux`

---

## 3. AI-Assisted & Agentic Testing ⭐ Key Differentiator

Be comfortable with agent-assisted and agentic workflows. Most SDETs don't have this yet.

### The Problem
At McAfee, the CI/CD pipeline generated hundreds of test failures per week. Triaging them — real regressions vs. environment noise vs. flakiness — consumed hours of engineering time every sprint. Engineers started ignoring the pipeline. That's the worst outcome in QE.

### LLM-Powered Failure Clustering

**How it works:**
1. Every test failure (error message, stack trace, test name) is sent to an LLM
2. The LLM reads all failures and groups them into clusters with plain-English labels:
   - *"34 failures — socket timeout, likely infra issue, not a code bug"*
   - *"12 failures — same null pointer on login service, real regression"*
   - *"8 failures — known flaky selector on download page, safe to retry"*
3. Engineers see 3 grouped buckets instead of a wall of 100 red tests

### Self-Healing Scripts
- For clusters the LLM marks "known flaky" with high confidence, tests auto-retry before being marked failed
- Tests that pass on retry are flagged as flaky and quarantined separately
- Pipeline stays red only for real issues

### Results
- **40% reduction** in manual triage time
- Two latent infrastructure issues surfaced that had been hiding in noise for months
- Engineers started trusting the pipeline again

### Tooling
- Built in Python with async LLM call batching for pipeline performance
- Integrated into Jenkins; cluster summaries surfaced in Grafana dashboards
- **ISTQB CT-GenAI certification** — exam scheduled May 2026

---

## 4. Production-Quality Test Code

> JD requirement: *"Write clear, maintainable, production-quality test code"*

**What this looks like in practice:**
- Code reviewed in PRs by engineers — same standards as application code
- Modular design — shared fixtures, page objects, data factories; no copy-paste scripts
- Version controlled and branched — tests ship with features, not after them
- Informative failure messages — when a test fails, it explains what broke and why

### Languages

| Language | Level | Where Used |
|---|---|---|
| Python | Expert | Primary language — all automation frameworks across 5 employers |
| TypeScript | Proficient | Playwright test suites at McAfee |
| C# | Proficient | McAfee (2014–2018) and BlackBerry — listed as JD nice-to-have |
| JavaScript | Proficient | Cypress, WebDriverIO, Protractor suites at Broadcom |
| SQL / NoSQL | Proficient | Data validation queries for high-volume pipeline verification |

### Scale
- 5,000+ automated test suites at McAfee (2014–2018)
- 95%+ coverage with minimal false positives
- Frameworks adopted and built on by 3+ squads — maintainability proven by others

---

## 5. Cross-Functional Collaboration

**How you work with engineers and PMs:**
- Embedded in Agile squads — present in refinement, planning, design reviews, and retrospectives
- Defines acceptance criteria with PMs and engineers **before** code is written
- Raises testability concerns during design — not after implementation
- Introduced consumer-driven contract testing across McAfee squads — required engineering buy-in, not just tooling
- Led lunch-and-learn sessions on dependency injection and testable design patterns

**Standardization across teams:**
- Standardized release processes across 3+ engineering squads at McAfee
- Created reusable automation libraries at Equitable Life — 25% reduction in maintenance overhead
- Built centralized reporting platform at Broadcom used by global distributed squads

---

## 6. Bridging to Digital Forensics

> No direct forensics experience — but security software is the closest possible adjacent domain.

| Your McAfee / Security Experience | Magnet Forensics Equivalent |
|---|---|
| Data integrity checks on security microservices | Digital evidence integrity — forensic data must be provably correct |
| Non-deterministic behavior detection in analytics pipelines | Complex device data parsing — edge cases in acquired evidence |
| Consumer-facing security for millions of users — zero tolerance for data loss | Investigative tools used in criminal cases — quality failures have legal consequences |
| API contract testing — behavior must be exact, not approximate | Forensic analysis APIs — results must be deterministic and defensible in court |

**The core discipline is identical:** high-stakes data, correctness is non-negotiable, and the cost of a missed defect is measured in real-world harm — not just user complaints.

---


| Contract / performance / reliability testing | ✅ Present | Consumer-driven contracts + load testing |
| Digital forensics domain knowledge | ⚠️ Adjacent | Security software — same data integrity stakes |
