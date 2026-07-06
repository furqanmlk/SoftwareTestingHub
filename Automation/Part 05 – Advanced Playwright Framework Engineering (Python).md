## Part 05 – Advanced Playwright Framework Engineering (Python)

---

# Table of Contents

1. Advanced Playwright Architecture
2. Browser, Context and Page
3. Fixture Scopes
4. Authentication Reuse (storage_state)
5. Network Interception & API Mocking
6. Locator Best Practices
7. Waiting Strategies
8. Debugging Playwright Tests
9. Trace Viewer
10. Performance Optimization
11. Flaky Test Prevention
12. Enterprise Coding Standards
13. Interview Questions (Q41-Q50)

---

# Why Advanced Playwright?

Writing Playwright tests is easy.

Building an enterprise-grade automation platform that is:

- Fast
- Reliable
- Maintainable
- Scalable

is much more challenging.

Senior Automation Engineers spend more time designing frameworks than writing individual tests.

---

# Playwright Architecture

Playwright follows a layered architecture.

```text
Playwright

│

├── Browser

│      Chromium

│      Firefox

│      WebKit

│

├── Browser Context

│      Session Isolation

│

├── Page

│      Browser Tab

│

└── Locator

       UI Element
```

---

# Browser vs Context vs Page

## Browser

A browser represents an entire browser process.

Example:

```python
browser = playwright.chromium.launch()
```

---

## Browser Context

A Browser Context is an isolated browser session.

Each context has its own:

- Cookies
- Local Storage
- Session Storage
- Authentication

Example

```python
context = browser.new_context()
```

Think of it as an Incognito Window.

---

## Page

A page represents one browser tab.

```python
page = context.new_page()
```

---

## Architecture Diagram

```text
Chromium Browser

│

├── Context 1

│      ├── Page 1

│      └── Page 2

│

├── Context 2

│      ├── Page 1

│      └── Page 2
```

---

# Why Browser Context Matters

Never share one browser session across all tests.

Instead

```text
Test 1

↓

Context 1

Test 2

↓

Context 2

Test 3

↓

Context 3
```

Benefits

- Independent execution
- No shared cookies
- Better parallel execution
- Reliable authentication

---

# Pytest Fixture Scopes

Pytest fixtures can be reused with different scopes.

| Scope | Lifetime |
|--------|----------|
| function | Every test |
| class | Every class |
| module | Every module |
| package | Every package |
| session | Entire execution |

---

## Example

```python
import pytest

@pytest.fixture(scope="session")
def config():
    return load_configuration()
```

---

## Which Scope Should You Use?

| Object | Recommended Scope |
|---------|-------------------|
| Configuration | Session |
| Browser | Session |
| Browser Context | Function |
| Page | Function |
| Test Data | Function |

---

## Interview Tip

Sharing the browser is acceptable.

Sharing browser contexts between tests is generally not recommended because it can introduce hidden dependencies and reduce test isolation.

---

# Authentication Reuse

Logging in before every test is inefficient.

Playwright allows authentication state to be reused.

```text
Login Once

↓

Save storage_state.json

↓

Reuse Authentication

↓

Run Hundreds of Tests
```

---

## Benefits

- Faster execution
- Stable authentication
- Reduced login failures
- Better CI/CD performance

---

## Example

```python
context = browser.new_context(
    storage_state="storage_state.json"
)
```

---

# Network Interception

Playwright can intercept network requests.

Example

```python
page.route(
    "**/users",
    lambda route: route.fulfill(
        status=200,
        body='{"name":"John"}'
    )
)
```

---

## Why Mock APIs?

Suppose

Backend

↓

Unavailable

UI Testing

↓

Blocked

Instead

```text
Mock API

↓

UI Continues

↓

Reliable Tests
```

---

## Enterprise Uses

- Third-party APIs
- Payment gateways
- Weather services
- Authentication providers
- Error simulation

---

# API Mocking

Mocking allows testing UI independently of backend availability.

Benefits

- Faster execution
- Stable tests
- Predictable responses
- Better negative testing

---

# Locator Best Practices

Preferred order:

1. get_by_role()
2. get_by_label()
3. get_by_placeholder()
4. get_by_text()
5. data-testid
6. CSS selector (when necessary)

---

## Good Example

```python
page.get_by_role(
    "button",
    name="Login"
).click()
```

---

## Acceptable Example

```python
page.get_by_test_id(
    "login-button"
).click()
```

---

## Avoid

```python
page.locator(
    "div:nth-child(4)"
)
```

or

```python
//*[@id='content']/div[2]/table/tr[4]/td[1]
```

These selectors are brittle and difficult to maintain.

---

# Waiting Strategies

Avoid fixed delays.

Bad

```python
page.wait_for_timeout(5000)
```

Good

```python
page.get_by_role(
    "button",
    name="Submit"
).click()

page.wait_for_url(
    "**/dashboard"
)
```

---

## Auto Waiting

One of Playwright's strengths is automatic waiting.

Playwright waits for:

- Visibility
- Stability
- Clickability
- Enabled state

before performing actions.

---

# Debugging Playwright Tests

Useful options

```bash
pytest -s
```

```bash
pytest --headed
```

```bash
pytest --slowmo=500
```

```bash
PWDEBUG=1 pytest
```

---

# Trace Viewer

Playwright can record every action.

```text
Click

↓

Navigation

↓

Network

↓

Console

↓

Screenshot

↓

DOM Snapshot
```

---

## Why Trace Viewer?

Instead of guessing why a test failed,

you can replay the entire execution.

---

# Screenshots

Capture screenshots on failures.

```python
page.screenshot(
    path="failure.png"
)
```

---

# Video Recording

Useful for intermittent failures.

Benefits

- Replay execution
- Visual debugging
- Easier defect analysis

---

# Performance Optimization

Large frameworks should minimize execution time.

Strategies

- Parallel execution
- Authentication reuse
- API setup
- Browser reuse
- Context isolation
- Dependency caching
- Selective test execution

---

# Flaky Test Prevention

Most flaky tests are caused by:

- Timing issues
- Dynamic elements
- Shared test data
- Environment instability
- Hardcoded waits
- Poor locators

---

## Best Practices

- Prefer role-based locators.
- Wait for application state rather than fixed time.
- Use isolated browser contexts.
- Keep tests independent.
- Avoid execution order dependencies.

---

# Enterprise Coding Standards

Every automation project should define coding standards.

Example

### Naming

Good

```text
test_create_user.py
```

Bad

```text
abc.py
```

---

### Method Names

Good

```python
login_as_admin()
```

Bad

```python
login123()
```

---

### Variable Names

Good

```python
user_name
```

Bad

```python
u1
```

---

### Comments

Write comments only when they explain *why*, not *what*.

Bad

```python
# Click button

page.click()
```

Good

```python
# Force logout to reset authentication state before the next scenario.
```

---

# Interview Questions

---

# Q41. Why does Playwright use Browser Contexts?

## Short Interview Answer

Browser Contexts provide isolated browser sessions, allowing tests to run independently without sharing cookies, sessions, or local storage.

---

## Senior Interview Answer

Using Browser Contexts ensures test isolation and enables reliable parallel execution. Each test receives a clean session, reducing flaky behavior caused by shared authentication or application state.

---

# Q42. Why should each test have its own Browser Context?

## Answer

Shared contexts create hidden dependencies between tests.

Independent contexts provide:

- Better reliability
- Parallel execution
- Test independence
- Easier debugging

---

# Q43. Why should you avoid `wait_for_timeout()`?

## Answer

Fixed waits slow execution and introduce instability.

Prefer waiting for application state using Playwright's built-in auto-waiting or explicit conditions such as:

- URL changes
- Element visibility
- Network completion
- Assertions

---

# Q44. What is Playwright Trace Viewer?

## Answer

Trace Viewer records the complete execution of a test, including UI actions, network requests, console logs, screenshots, and DOM snapshots. It allows engineers to replay failures and identify the root cause efficiently.

---

# Q45. How would you reduce execution time in a Playwright framework?

## Strong Interview Answer

I would enable parallel execution with `pytest-xdist`, reuse authentication through `storage_state`, execute API setup instead of repetitive UI setup, optimize fixtures, use browser contexts for isolation, cache dependencies in CI/CD, and ensure tests remain independent so they can run concurrently.

---

# Q46. What makes Playwright more reliable than older UI automation tools?

## Answer

Playwright improves reliability through:

- Automatic waiting
- Browser context isolation
- Modern locator strategies
- Native support for Chromium, Firefox, and WebKit
- Built-in tracing, screenshots, and video recording
- Powerful network interception and API mocking

---

# Q47. How do you debug intermittent failures?

## Strong Interview Answer

I review Playwright trace files, screenshots, videos, and logs to understand where the failure occurred. I verify whether the issue is caused by timing, unstable locators, test data, or environment problems. I then reproduce the issue locally before implementing a fix.

---

# Q48. How should enterprise teams organize Playwright tests?

## Answer

Tests should be organized by business capability rather than by page or component.

Example:

```text
tests/

├── authentication/

├── users/

├── orders/

├── billing/

├── reporting/
```

This structure aligns automation with business domains and improves maintainability.

---

# Q49. What is the biggest mistake teams make when building Playwright frameworks?

## Strong Interview Answer

One common mistake is allowing business logic, locators, waits, and assertions to become tightly coupled within test files. This leads to duplication and makes maintenance difficult. A well-designed framework separates responsibilities into page objects, fixtures, utilities, configuration, and test layers.

---

# Q50. If you were designing a Playwright framework from scratch today, what would it include?

## Strong Interview Answer

I would build a modular framework using Python, Pytest, and Playwright. It would include Page Objects, reusable fixtures, configuration management with YAML, centralized logging, Allure reporting, API clients, test data builders, authentication reuse, browser context isolation, parallel execution, GitHub Actions integration, and clear coding standards. The framework would emphasize maintainability, scalability, and fast feedback in CI/CD.

---

# Quick Revision

Remember these concepts:

- Browser
- Browser Context
- Page
- Fixture Scope
- storage_state
- Network Interception
- API Mocking
- Auto Waiting
- Trace Viewer
- Parallel Execution
- Test Isolation
- Role-based Locators
- Business-driven Test Organization
- Clean Architecture
