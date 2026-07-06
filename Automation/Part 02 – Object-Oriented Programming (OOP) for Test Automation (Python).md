## Part 02 – Object-Oriented Programming (OOP) for Test Automation (Python)

---

# Table of Contents

1. Why OOP Matters in Test Automation
2. OOP Principles
3. Classes & Objects
4. Encapsulation
5. Inheritance
6. Polymorphism
7. Abstraction
8. Composition vs Inheritance
9. Interface vs Abstract Class (Python Perspective)
10. SOLID Principles
11. Interview Questions (Q11–Q20)

---

# Why OOP Matters in Test Automation

Modern automation frameworks are software applications.

A well-designed framework should be:

- Reusable
- Scalable
- Easy to maintain
- Easy to extend
- Easy to debug

Without OOP:

```text
500 Playwright scripts

↓

Duplicate code

↓

Hard to maintain

↓

Expensive
```

With OOP:

```text
Reusable Classes

↓

Reusable Methods

↓

Maintainable Framework

↓

Lower Maintenance Cost
```

---

# OOP Principles

Object-Oriented Programming consists of four main principles:

1. Encapsulation
2. Inheritance
3. Polymorphism
4. Abstraction

A fifth concept, **Composition**, is equally important for designing automation frameworks.

---

# Class and Object

## What is a Class?

A class is a blueprint that defines the properties (attributes) and behaviors (methods) of an object.

Think of a class as a template.

Example:

```python
class LoginPage:

    def login(self, username, password):
        print(f"Logging in as {username}")
```

---

## What is an Object?

An object is an instance of a class.

```python
page = LoginPage()

page.login("admin", "password123")
```

---

## Real Framework Example

```text
BasePage

↓

LoginPage

↓

DashboardPage

↓

SettingsPage
```

Each page is represented as a class.

---

# Encapsulation

## Definition

Encapsulation is the practice of keeping data and behavior together while restricting direct access to internal implementation details.

---

## Why Encapsulation?

Instead of exposing everything:

```python
driver.find_element(...)
driver.find_element(...)
driver.find_element(...)
```

Expose one reusable method:

```python
class LoginPage:

    def login(self, username, password):
        self.enter_username(username)
        self.enter_password(password)
        self.click_login()
```

Now the test only calls:

```python
login_page.login("admin", "password123")
```

---

## Benefits

- Cleaner code
- Better readability
- Easier maintenance
- Lower duplication

---

# Inheritance

## Definition

Inheritance allows one class to reuse properties and methods from another class.

---

## Example

```python
class BasePage:

    def click(self, locator):
        print(f"Clicking {locator}")


class LoginPage(BasePage):

    def login(self):
        self.click("Login Button")
```

---

## Framework Example

```text
BasePage

├── LoginPage

├── DashboardPage

├── UserPage

└── CheckoutPage
```

Every page automatically inherits common methods.

---

## Benefits

- Code reuse
- Centralized changes
- Reduced duplication

---

# Polymorphism

## Definition

Polymorphism allows different classes to implement the same method differently.

---

## Example

```python
class ChromeBrowser:

    def launch(self):
        print("Launching Chrome")


class FirefoxBrowser:

    def launch(self):
        print("Launching Firefox")
```

Usage:

```python
browsers = [
    ChromeBrowser(),
    FirefoxBrowser()
]

for browser in browsers:
    browser.launch()
```

Output

```text
Launching Chrome

Launching Firefox
```

---

## Automation Example

Different browsers can implement the same interface while behaving differently internally.

---

# Abstraction

## Definition

Abstraction hides implementation details and exposes only necessary functionality.

Users don't need to know *how* login works.

They simply call:

```python
login_page.login()
```

---

## Example

```python
from abc import ABC, abstractmethod

class Browser(ABC):

    @abstractmethod
    def launch(self):
        pass
```

Implementation

```python
class Chrome(Browser):

    def launch(self):
        print("Launching Chrome")
```

---

## Benefits

- Cleaner APIs
- Easier maintenance
- Flexible implementation

---

# Composition vs Inheritance

## Composition

A class **has another object**.

```python
class LoginPage:

    def __init__(self, driver):
        self.driver = driver
```

The LoginPage **has a WebDriver**.

---

## Inheritance

A class **is another class**.

```python
class LoginPage(BasePage):
    pass
```

---

## Which is Better?

Modern frameworks generally prefer **composition over inheritance**.

Why?

Because composition is:

- More flexible
- Loosely coupled
- Easier to test
- Easier to maintain

---

# Interface vs Abstract Class (Python)

Python does not have a dedicated `interface` keyword like Java or C#.

Instead, we typically use **Abstract Base Classes (ABC)** from the `abc` module.

Example:

```python
from abc import ABC, abstractmethod

class Browser(ABC):

    @abstractmethod
    def launch(self):
        pass
```

Implementation:

```python
class ChromeBrowser(Browser):

    def launch(self):
        print("Launching Chrome")
```

---

# SOLID Principles

Senior interviewers frequently ask about SOLID.

| Principle | Meaning |
|-----------|---------|
| S | Single Responsibility Principle |
| O | Open/Closed Principle |
| L | Liskov Substitution Principle |
| I | Interface Segregation Principle |
| D | Dependency Inversion Principle |

---

## Single Responsibility Principle

A class should have only one responsibility.

Bad:

```text
LoginPage

↓

Login

↓

Database

↓

Reporting

↓

Screenshot

↓

API Calls
```

Good:

```text
LoginPage

↓

Login Only
```

---

## Open/Closed Principle

Software should be open for extension but closed for modification.

Instead of changing existing code, create a new implementation.

---

## Dependency Inversion Principle

Depend on abstractions instead of concrete implementations.

Instead of:

```python
page = ChromeBrowser()
```

Depend on:

```python
page = Browser()
```

---

# Interview Questions

---

# Q11. Why is OOP important in Test Automation?

## Short Interview Answer

Object-Oriented Programming enables automation frameworks to be reusable, maintainable, scalable, and easier to extend.

---

## Senior Interview Answer

> Enterprise automation frameworks often contain thousands of test cases. OOP helps organize the framework into reusable classes, reducing code duplication and simplifying maintenance. It also enables design patterns such as the Page Object Model and promotes clean architecture.

---

## Real Project Example

In a Selenium framework, common WebDriver operations such as clicking elements, waiting for visibility, and taking screenshots are implemented once in a `BasePage` class. Individual page classes inherit or compose these shared capabilities, avoiding duplication across the framework.

---

# Q12. What is a Class?

## Short Interview Answer

A class is a blueprint that defines the attributes and methods of an object.

Example:

```python
class LoginPage:

    def login(self):
        print("Login")
```

---

# Q13. What is an Object?

## Short Interview Answer

An object is an instance of a class.

```python
page = LoginPage()

page.login()
```

---

# Q14. What is Encapsulation?

## Short Interview Answer

Encapsulation hides implementation details and exposes only the methods necessary for other parts of the framework to use.

Example:

```python
login_page.login(username, password)
```

The test does not need to know how the individual fields are located or interacted with.

---

# Q15. What is Inheritance?

## Short Interview Answer

Inheritance allows a child class to reuse methods and properties from a parent class.

Example:

```python
class BasePage:

    def click(self):
        pass


class LoginPage(BasePage):
    pass
```

---

# Q16. What is Polymorphism?

## Short Interview Answer

Polymorphism allows different classes to provide their own implementation of the same method.

Example:

```python
browser.launch()
```

can launch Chrome, Firefox, or Edge depending on the object passed.

---

# Q17. What is Abstraction?

## Short Interview Answer

Abstraction hides implementation details while exposing a simple interface.

Example:

```python
login_page.login()
```

The caller doesn't need to know how the login steps are implemented internally.

---

# Q18. Composition vs Inheritance?

## Senior Interview Answer

Composition is generally preferred because it creates loosely coupled, modular classes. Inheritance is useful for sharing truly common behavior, but excessive inheritance can make frameworks rigid and difficult to maintain.

---

# Q19. Explain SOLID Principles.

## Expected Interview Answer

SOLID is a set of object-oriented design principles that improve maintainability, extensibility, and testability.

Automation frameworks following SOLID are easier to scale and modify as applications evolve.

---

# Q20. Which OOP concepts are most commonly used in Selenium or Playwright frameworks?

## Strong Interview Answer

The most frequently used concepts are:

- Classes and Objects
- Encapsulation
- Composition
- Inheritance (used selectively)
- Abstraction
- SOLID Principles

Modern automation frameworks also rely heavily on composition and dependency injection to improve flexibility and reduce coupling.

---

# Quick Revision

Remember these keywords:

- Class
- Object
- Encapsulation
- Inheritance
- Polymorphism
- Abstraction
- Composition
- SOLID
- BasePage
- Page Object Model
- Reusability
- Maintainability
- Loose Coupling
- Dependency Injection
