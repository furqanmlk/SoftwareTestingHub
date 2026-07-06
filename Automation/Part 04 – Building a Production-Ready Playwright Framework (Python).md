## Part 04 – Building a Production-Ready Playwright Framework (Python)

---

# Table of Contents

1. Framework Design Goals
2. Framework Architecture
3. Project Folder Structure
4. Configuration Management
5. Pytest Fixtures
6. Browser Management
7. Page Object Layer
8. Test Layer
9. Utilities Layer
10. API Layer
11. Reporting
12. Logging
13. Test Data Management
14. Parallel Execution
15. Interview Questions (Q31–Q40)

---

# Why Framework Architecture Matters

Many automation engineers can write Playwright scripts.

Senior Automation Engineers build frameworks.

A good framework should be:

- Maintainable
- Scalable
- Reusable
- Readable
- Configurable
- CI/CD Ready
- Parallel Execution Ready
- API Ready
- Cloud Ready

---

# Enterprise Framework Architecture

```text
                    Test Suite
                        │
                        ▼
                 Pytest Test Cases
                        │
                        ▼
                Page Object Layer
                        │
                        ▼
              Playwright Page Object
                        │
                        ▼
             Browser / Context / Page
                        │
                        ▼
                   Application
```

Supporting Components

```text
Configuration

↓

Fixtures

↓

Logging

↓

Reporting

↓

API Clients

↓

Utilities

↓

Test Data

↓

CI/CD
```

---

# Recommended Folder Structure

```text
automation-framework/

│

├── config/
│   ├── config.py
│   ├── settings.yaml
│   └── environments.py
│

├── pages/
│   ├── base_page.py
│   ├── login_page.py
│   ├── dashboard_page.py
│   └── users_page.py
│

├── api/
│   ├── base_api.py
│   └── users_api.py
│

├── builders/
│   ├── user_builder.py
│   └── order_builder.py
│

├── fixtures/
│   ├── browser.py
│   └── api_client.py
│

├── utils/
│   ├── logger.py
│   ├── helpers.py
│   ├── wait_utils.py
│   └── screenshot.py
│

├── testdata/
│   ├── users.json
│   └── products.json
│

├── tests/
│   ├── ui/
│   ├── api/
│   └── integration/
│

├── reports/
│

├── conftest.py

├── pytest.ini

├── requirements.txt

└── README.md
```

---

# Why This Structure?

Each folder has one responsibility.

Example

pages/

↓

Only UI interaction

tests/

↓

Only assertions

utils/

↓

Reusable utilities

api/

↓

REST API calls

builders/

↓

Generate test data

This follows the Single Responsibility Principle (SRP).

---

# Configuration Management

Never hardcode values.

Bad

```python
page.goto("https://qa.company.com")
```

Good

```python
BASE_URL = config.base_url

page.goto(BASE_URL)
```

---

# Example settings.yaml

```yaml
environment: qa

base_url: https://qa.company.com

browser: chromium

headless: true

timeout: 30000
```

---

# Loading Configuration

```python
import yaml

with open("config/settings.yaml") as file:
    config = yaml.safe_load(file)

print(config["base_url"])
```

---

# Why YAML?

Advantages

- Human-readable
- Environment-specific
- Version controlled
- Easy to maintain

---

# Browser Fixture

Playwright works naturally with Pytest fixtures.

Example

```python
import pytest
from playwright.sync_api import sync_playwright


@pytest.fixture
def page():

    with sync_playwright() as p:

        browser = p.chromium.launch()

        page = browser.new_page()

        yield page

        browser.close()
```

---

# Why Fixtures?

Without fixtures

Every test creates browsers manually.

With fixtures

Pytest manages setup and teardown automatically.

Benefits

- Cleaner tests
- Less duplication
- Better resource management

---

# Base Page

Every page shares common functionality.

Example

```python
class BasePage:

    def __init__(self, page):

        self.page = page

    def click(self, locator):

        self.page.locator(locator).click()

    def fill(self, locator, value):

        self.page.locator(locator).fill(value)
```

---

# Login Page

```python
class LoginPage(BasePage):

    USERNAME = "#username"

    PASSWORD = "#password"

    LOGIN = "#login"

    def login(self, username, password):

        self.fill(self.USERNAME, username)

        self.fill(self.PASSWORD, password)

        self.click(self.LOGIN)
```

---

# Test Case

```python
def test_login(page):

    login = LoginPage(page)

    login.login(

        "admin",

        "password123"

    )
```

Notice

The test contains business logic.

The page contains UI logic.

---

# Utilities Layer

Utilities contain reusable helper methods.

Examples

```text
Logger

Screenshot

Date Utils

Random Data

File Utils

JSON Utils

Retry Logic
```

Utilities should never contain business logic.

---

# API Layer

Modern frameworks combine UI and API testing.

Structure

```text
tests/

↓

API Layer

↓

Requests / HTTPX

↓

Application API
```

Example

```python
class UsersApi:

    def create_user(self):

        ...
```

UI tests can prepare data through APIs before opening the browser.

---

# Logging

Every framework should generate useful logs.

Example

```
INFO

Launching browser

INFO

Opening Login Page

INFO

Entering Username

INFO

Click Login

INFO

Dashboard Loaded
```

Benefits

- Easier debugging

- Better reporting

- Audit trail

---

# Reporting

Recommended

- Allure

- Playwright HTML Report

Include

- Screenshots

- Videos

- Logs

- Trace files

- Environment

- Test duration

---

# Test Data Management

Never hardcode test data.

Bad

```python
username = "admin"
```

Better

```python
user = UserBuilder().admin().build()
```

or

```python
user = load_json("users.json")
```

---

# Parallel Execution

Pytest supports parallel execution.

Example

```bash
pytest -n 4
```

Benefits

- Faster execution

- Better CI/CD performance

- Lower execution cost

---

# Interview Questions

---

# Q31. What makes a good automation framework?

## Short Interview Answer

A good framework is modular, maintainable, scalable, reusable, configurable, and easy for the team to understand.

---

## Senior Interview Answer

A production-ready framework should separate concerns into distinct layers, use design patterns such as the Page Object Model and Dependency Injection, centralize configuration, support parallel execution, integrate with CI/CD, and provide comprehensive reporting and logging.

---

# Q32. Why use Pytest fixtures?

## Answer

Fixtures manage test setup and teardown automatically.

Benefits

- Cleaner tests

- Dependency Injection

- Reusability

- Better resource management

---

# Q33. Why create a Base Page?

## Answer

A Base Page centralizes common browser operations such as clicking, typing, waiting, and navigation. This reduces duplication and ensures consistent behavior across all page objects.

---

# Q34. Why separate Pages from Tests?

## Answer

Tests should express business behavior, while page objects encapsulate UI implementation details.

If a locator changes, only the page class should be updated.

---

# Q35. Why should configuration be externalized?

## Answer

External configuration enables the same framework to run against multiple environments without code changes.

Examples include:

- Browser
- Base URL
- Credentials
- Timeouts
- API endpoints

---

# Q36. Why should UI and API automation share one framework?

## Answer

Combining UI and API automation improves efficiency. API calls can prepare test data, validate backend behavior, or clean up data, reducing dependence on slow UI interactions.

---

# Q37. Why use builders for test data?

## Answer

Builders generate consistent, reusable test data while avoiding duplication and improving readability.

---

# Q38. What should never be placed in test files?

Avoid:

- Locators
- Wait logic
- Business workflows
- Configuration
- Hardcoded credentials

Tests should focus on assertions and business scenarios.

---

# Q39. How would you organize a framework for a team of 20 automation engineers?

## Strong Interview Answer

I would separate the framework into layers for pages, APIs, fixtures, utilities, configuration, builders, and tests. I'd enforce coding standards, centralize configuration, implement code reviews, integrate Allure reporting, enable parallel execution, and use GitHub Actions for continuous integration. This architecture allows multiple engineers to work independently while maintaining consistency and minimizing merge conflicts.

---

# Q40. How would you improve an existing Playwright framework?

## Strong Interview Answer

I would first evaluate maintainability, duplication, execution time, and flakiness. I'd centralize configuration, adopt the Page Object Model if not already in place, introduce dependency injection with Pytest fixtures, improve logging and reporting, remove duplicated logic, enable parallel execution, and integrate API utilities to reduce unnecessary UI interactions.

---

# Framework Checklist

A production-ready framework should include:

- Page Object Model
- Base Page
- Configuration Management
- Pytest Fixtures
- Logging
- Allure Reporting
- API Layer
- Builders
- Utilities
- Parallel Execution
- GitHub Actions Integration
- Environment Support
- Trace Files
- Screenshots
- CI/CD Ready

---

# Quick Revision

Remember these keywords:

- Pytest
- Fixtures
- Base Page
- Configuration
- YAML
- Logging
- Allure
- Builders
- API Layer
- Utilities
- Dependency Injection
- Parallel Execution
- Separation of Concerns
- Single Responsibility Principle
