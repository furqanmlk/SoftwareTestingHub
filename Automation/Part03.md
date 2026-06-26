# Senior QA Automation Architect Interview Handbook

# Chapter 02 – Automation Script Development

## Part 03 – Design Patterns for Modern Playwright Frameworks (Python)

---

# Table of Contents

1. Why Design Patterns Matter
2. Page Object Model (POM)
3. Factory Pattern
4. Singleton Pattern
5. Builder Pattern
6. Strategy Pattern
7. Facade Pattern
8. Dependency Injection
9. Composition over Inheritance
10. Framework Architecture
11. Interview Questions (Q21–Q30)

---

# Why Design Patterns Matter

Large automation projects quickly become difficult to maintain without a consistent architecture.

Imagine:

```text
500 Tests

↓

5 Developers

↓

10,000 Lines of Code

↓

No Design Pattern

↓

Duplicate Code

↓

High Maintenance

↓

Slow Development
```

Using design patterns creates:

- Reusable code
- Better readability
- Easier maintenance
- Team consistency
- Scalability

---

# Page Object Model (POM)

## Definition

The Page Object Model is a design pattern where every application page is represented by a Python class.

Instead of writing UI interaction directly in tests, all page-specific logic lives inside Page Objects.

---

## Without POM

```python
def test_login(page):
    page.goto("https://app.example.com")

    page.locator("#username").fill("admin")
    page.locator("#password").fill("password")
    page.locator("#login").click()

    assert page.locator("text=Dashboard").is_visible()
```

Problems:

- Duplicate locators
- Difficult maintenance
- Low readability

---

## With POM

### LoginPage.py

```python
class LoginPage:

    def __init__(self, page):
        self.page = page

    def login(self, username, password):
        self.page.locator("#username").fill(username)
        self.page.locator("#password").fill(password)
        self.page.locator("#login").click()
```

---

### Test

```python
def test_login(login_page):

    login_page.login(
        "admin",
        "password123"
    )
```

---

## Benefits

- Centralized locators
- Better readability
- Easy maintenance
- Code reuse

---

## Interview Tip

Every enterprise Playwright framework should use some variation of the Page Object Model.

---

# Factory Pattern

## Definition

The Factory Pattern creates objects without exposing object creation logic to the client.

Instead of writing:

```python
browser = chromium.launch()
```

Use:

```python
browser = BrowserFactory.create("chrome")
```

---

## Example

```python
class BrowserFactory:

    @staticmethod
    def create(browser_name):

        if browser_name == "chromium":
            return "Chromium"

        if browser_name == "firefox":
            return "Firefox"

        if browser_name == "webkit":
            return "WebKit"

        raise ValueError("Unsupported browser")
```

---

## Why Use Factory?

Instead of changing test code:

```python
browser = BrowserFactory.create(browser)
```

The implementation stays in one place.

---

## Enterprise Usage

Factories are commonly used for:

- Browser creation
- API clients
- Database connections
- Environment configuration
- Test data generation

---

# Singleton Pattern

## Definition

Singleton ensures only one instance of an object exists during execution.

Example:

```text
One Configuration

↓

All Tests
```

---

## Example

```python
class Config:

    _instance = None

    def __new__(cls):

        if cls._instance is None:
            cls._instance = super().__new__(cls)

        return cls._instance
```

---

## Typical Usage

- Configuration
- Logger
- Report Manager
- Test Settings

---

## Interview Tip

Singleton is useful for shared resources, but avoid overusing it because it can make testing harder.

---

# Builder Pattern

## Definition

Builder creates complex objects step by step.

Instead of:

```python
User(
    "John",
    "Smith",
    "john@email.com",
    True,
    "Admin"
)
```

Use

```python
user = (
    UserBuilder()
    .name("John")
    .email("john@email.com")
    .role("Admin")
    .active(True)
    .build()
)
```

---

## Why?

- Cleaner code
- Easier to read
- Easier to extend
- Optional fields

---

## Common Automation Usage

Builder is useful for:

- Test data
- API payloads
- User profiles
- Orders
- Database objects

---

# Strategy Pattern

## Definition

Strategy allows selecting behavior at runtime.

Instead of:

```text
if Chrome

if Firefox

if WebKit
```

Each browser has its own strategy.

---

## Example

```python
class BrowserStrategy:

    def launch(self):
        pass
```

Implementation

```python
class ChromiumStrategy(BrowserStrategy):

    def launch(self):
        print("Chromium")
```

---

## Benefits

- Cleaner code
- Easier maintenance
- Easily extendable

---

# Facade Pattern

## Definition

Facade provides one simple interface to a complex system.

Instead of:

```python
page.goto(...)

page.fill(...)

page.click(...)

page.wait_for_url(...)
```

Expose one method:

```python
login.login_as_admin()
```

---

## Benefits

- Simple API
- Better readability
- Less duplicate code

---

# Dependency Injection

## Definition

Dependency Injection means objects receive their dependencies instead of creating them.

Bad

```python
class LoginPage:

    def __init__(self):

        self.page = Page()
```

Good

```python
class LoginPage:

    def __init__(self, page):

        self.page = page
```

---

## Why?

Dependency Injection makes:

- Unit testing easier
- Mocking easier
- Framework more flexible
- Components loosely coupled

---

## Playwright Example

```python
@pytest.fixture
def login_page(page):

    return LoginPage(page)
```

The fixture injects the dependency.

---

# Composition over Inheritance

Modern Python frameworks prefer:

Composition

instead of

Deep inheritance.

Instead of

```text
BasePage

↓

LoginPage

↓

AdminLoginPage

↓

AdminDashboard
```

Prefer

```text
LoginPage

↓

Uses

↓

Page

↓

Logger

↓

Config

↓

API Client
```

Each component has a single responsibility.

---

# Example Framework Structure

```text
framework/

│

├── pages/

│      login_page.py

│      dashboard_page.py

│

├── api/

│      users_api.py

│

├── utils/

│      logger.py

│      config.py

│

├── builders/

│      user_builder.py

│

├── fixtures/

│      browser.py

│

├── tests/

│      test_login.py

│

└── conftest.py
```

---

# Interview Questions

---

# Q21. Why is the Page Object Model important?

## Short Interview Answer

The Page Object Model improves maintainability by separating page interactions from test logic.

---

## Senior Interview Answer

> POM centralizes locators and page-specific behavior into reusable classes. When the UI changes, only the page class requires modification rather than every individual test. This significantly reduces maintenance effort in large Playwright projects.

---

## Real Example

If the login button locator changes:

Without POM

Update 150 tests.

With POM

Update one method.

---

# Q22. Why should locators never appear in test files?

## Answer

Tests should describe business behavior, not implementation details.

Good:

```python
login_page.login(user)
```

Bad:

```python
page.locator(...)
page.locator(...)
page.locator(...)
```

---

# Q23. When would you use a Factory Pattern?

## Answer

Factory is useful whenever object creation depends on configuration or runtime conditions.

Examples:

- Browser selection
- API clients
- Database connections
- Environment-specific services

---

# Q24. What is Dependency Injection?

## Answer

Dependency Injection means dependencies are provided to an object instead of being created internally.

Benefits:

- Loose coupling
- Easier testing
- Better modularity

---

# Q25. Why is Composition preferred over Inheritance?

## Answer

Composition produces flexible, modular code with fewer dependencies between classes. It avoids deep inheritance hierarchies that become difficult to maintain.

---

# Q26. What is the Builder Pattern?

## Answer

Builder creates complex objects through a readable, step-by-step process. It is especially useful for creating API request payloads and test data.

---

# Q27. What is the Strategy Pattern?

## Answer

Strategy allows behavior to change dynamically without modifying the client code. It is commonly used for browser-specific logic, authentication methods, or environment-specific workflows.

---

# Q28. What is the Facade Pattern?

## Answer

Facade hides complex implementation details behind a simple interface, making tests easier to read and maintain.

---

# Q29. Which design patterns do you use most often in Playwright frameworks?

## Strong Interview Answer

The patterns I use most frequently are:

- Page Object Model
- Factory
- Dependency Injection
- Builder
- Facade
- Composition

These patterns keep the framework modular, maintainable, and scalable as the number of tests grows.

---

# Q30. How would you design a scalable Playwright framework?

## Strong Interview Answer

I would organize the framework into separate layers for pages, fixtures, utilities, API clients, configuration, builders, and tests. I'd use the Page Object Model for UI interactions, dependency injection through Pytest fixtures, composition over inheritance, centralized configuration, Allure reporting, and GitHub Actions for CI/CD. This architecture promotes reuse, minimizes duplication, and makes the framework easier to extend.

---

# Quick Revision

Remember these patterns:

- Page Object Model
- Factory
- Singleton
- Builder
- Strategy
- Facade
- Dependency Injection
- Composition
- SOLID Principles
- Loose Coupling
- High Cohesion
