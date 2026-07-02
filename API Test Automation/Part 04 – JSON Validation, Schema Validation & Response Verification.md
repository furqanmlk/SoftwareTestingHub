## Part 04 – JSON Validation, Schema Validation & Response Verification

---

# Table of Contents

1. Why Response Validation Matters
2. Levels of API Validation
3. JSON Validation
4. Field Validation
5. Nested Object Validation
6. Array Validation
7. Optional vs Required Fields
8. JSON Schema Validation
9. Pydantic Model Validation
10. Business Rule Validation
11. Response Time Validation
12. Header Validation
13. Contract Validation
14. Validation Framework Design
15. Interview Questions (Q46-Q60)

---

# Why Response Validation Matters

Many automation engineers stop after checking the status code.

Example:

```python
assert response.status_code == 200
```

This is **not enough**.

A successful status code does not guarantee that the API returned the correct data.

A proper API validation should verify:

- Status code
- Headers
- JSON structure
- Field values
- Business rules
- Schema
- Response time

---

# Validation Pyramid

```text
                    Business Rules
                          ▲
                    Schema Validation
                          ▲
                    Field Validation
                          ▲
                  Status Code Validation
```

As you move higher, validation becomes more meaningful.

---

# Example Response

```json
{
  "id": 101,
  "firstName": "John",
  "lastName": "Smith",
  "email": "john@email.com",
  "active": true,
  "roles": [
    "Admin",
    "Manager"
  ]
}
```

---

# Level 1 — Status Code Validation

```python
assert response.status_code == 200
```

Necessary but not sufficient.

---

# Level 2 — Response Body Validation

```python
data = response.json()

assert data["firstName"] == "John"

assert data["active"] is True
```

---

# Level 3 — Data Type Validation

Don't only validate values.

Validate types.

```python
assert isinstance(
    data["id"],
    int
)

assert isinstance(
    data["email"],
    str
)

assert isinstance(
    data["roles"],
    list
)
```

---

# Why Validate Types?

Imagine the API suddenly returns:

```json
{
  "id": "101"
}
```

instead of

```json
{
  "id": 101
}
```

Your UI might still work today, but another service could fail because it expects an integer.

---

# Nested Object Validation

Example

```json
{
  "user": {
    "id": 1,
    "profile": {
      "country": "Canada",
      "city": "Waterloo"
    }
  }
}
```

Python

```python
data = response.json()

assert data["user"]["profile"]["country"] == "Canada"
```

---

# Array Validation

Example

```json
{
  "roles": [
    "Admin",
    "Manager",
    "QA"
  ]
}
```

Validation

```python
roles = data["roles"]

assert len(roles) == 3

assert "Admin" in roles
```

---

# Optional Fields

Some fields may not always exist.

Example

```json
{
  "phone": null
}
```

Validation

```python
phone = data.get("phone")

if phone is not None:
    assert isinstance(phone, str)
```

---

# Required Fields

Some fields must always exist.

```python
required_fields = [

    "id",

    "email",

    "firstName"

]

for field in required_fields:

    assert field in data
```

---

# JSON Schema Validation

Schema validation verifies the entire JSON structure.

Instead of validating fields individually:

```python
assert data["id"] == 100

assert data["name"] == "John"
```

Validate everything using a schema.

---

# Example Schema

```python
user_schema = {

    "type": "object",

    "properties": {

        "id": {

            "type":"integer"

        },

        "email": {

            "type":"string"

        }

    },

    "required":[

        "id",

        "email"

    ]
}
```

---

# Validation

```python
from jsonschema import validate

validate(

    instance=data,

    schema=user_schema

)
```

---

# Why Use JSON Schema?

Advantages

- Detects missing fields
- Detects incorrect types
- Detects unexpected properties
- Improves maintainability
- Reusable

---

# Pydantic Validation

Modern Python frameworks often prefer Pydantic.

Example

```python
from pydantic import BaseModel

class User(BaseModel):

    id: int

    firstName: str

    email: str

    active: bool
```

Validation

```python
user = User(

    **response.json()

)
```

---

# Why Pydantic?

Advantages

- Type validation
- Better readability
- IDE support
- Cleaner code
- Automatic validation

---

# Invalid Example

Suppose API returns

```json
{
  "id":"abc"
}
```

Pydantic automatically raises:

```text
ValidationError
```

---

# Business Rule Validation

Schema validation checks structure.

Business validation checks correctness.

Example

API

```json
{

"price":100,

"discount":150

}
```

Schema

✔ Valid

Business Rule

❌ Invalid

Discount cannot exceed price.

---

# Business Validation Example

```python
assert data["discount"] <= data["price"]
```

---

# Date Validation

Example

```json
{

"createdAt":"2026-07-01"

}
```

Validation

```python
from datetime import datetime

datetime.strptime(

    data["createdAt"],

    "%Y-%m-%d"

)
```

---

# Email Validation

```python
assert "@" in data["email"]
```

Better

```python
from email_validator import validate_email

validate_email(

    data["email"]

)
```

---

# Response Time Validation

Always validate performance.

Example

```python
assert response.elapsed.total_seconds() < 2
```

Enterprise systems often define Service Level Objectives (SLOs).

Example

| API | Maximum Response Time |
|------|-----------------------|
| Login | 500 ms |
| Search | 1 sec |
| Reports | 3 sec |

---

# Header Validation

Example

```python
assert response.headers["Content-Type"] == "application/json"
```

Other headers

- Cache-Control
- ETag
- Content-Length
- Correlation-ID
- Location

---

# Response Length Validation

Example

```python
users = response.json()

assert len(users) > 0
```

---

# Contract Validation

Contract validation ensures the API follows its published specification.

Typical checks:

- Endpoint exists
- Required fields
- Correct data types
- Status codes
- Response structure

Later we'll cover OpenAPI and Pact in detail.

---

# Enterprise Validation Framework

```text
API Response

↓

Status Validator

↓

Header Validator

↓

Schema Validator

↓

Business Validator

↓

Performance Validator

↓

Report
```

Each validator should have one responsibility.

---

# Validation Utilities

Instead of repeating assertions:

```python
assert response.status_code == 200

assert response.headers["Content-Type"] == "application/json"

assert response.elapsed.total_seconds() < 2
```

Create reusable methods.

```python
ResponseValidator.validate_success(response)
```

---

# Interview Questions

---

# Q46. Why isn't validating only the status code enough?

## Short Interview Answer

Because a successful HTTP status code does not guarantee the returned data is correct.

---

## Senior Interview Answer

A response can return HTTP 200 while containing incorrect values, missing fields, invalid data types, or business rule violations. Enterprise API testing should validate the entire response, not just the status code.

---

# Q47. What should every API response validation include?

- Status code
- Headers
- JSON body
- Required fields
- Data types
- Business rules
- Response time
- Schema

---

# Q48. JSON Schema vs Pydantic?

| JSON Schema | Pydantic |
|-------------|-----------|
| Standard | Python-native |
| External file possible | Python classes |
| Contract validation | Object validation |
| Cross-platform | Python only |

---

# Q49. Why use Pydantic?

Pydantic provides automatic type validation, cleaner code, and strongly typed models, making API automation easier to maintain.

---

# Q50. What is Business Rule Validation?

Business Rule Validation verifies that returned data makes logical sense according to business requirements.

Example

Price

100

Discount

150

Schema

✔ Valid

Business Rule

❌ Invalid

---

# Q51. How would you validate nested JSON?

Navigate through the object hierarchy and validate values, types, and required fields at each level.

---

# Q52. How would you validate arrays?

Validate:

- Length
- Order (if applicable)
- Element type
- Required values
- Duplicate entries
- Sorting

---

# Q53. How would you validate response headers?

Validate:

- Content-Type
- Cache-Control
- Correlation-ID
- Security headers
- Content-Length
- Location (for resource creation)

---

# Q54. How do you validate response performance?

Measure response time and compare it against predefined service level objectives (SLOs).

Example

```python
assert response.elapsed.total_seconds() < 2
```

---

# Q55. What is Contract Validation?

Contract validation ensures the implementation matches the published API specification, including endpoints, request formats, response formats, and status codes.

---

# Q56. Why create reusable validators?

Reusable validators reduce duplication, improve consistency, and make future maintenance easier.

---

# Q57. How would you design a validation framework?

## Strong Interview Answer

I would separate validation into reusable components responsible for status codes, headers, schemas, business rules, and performance. Tests would focus on business scenarios while validator classes encapsulate common assertions.

---

# Q58. How do you handle optional fields?

Use `.get()` or equivalent access methods, validate the type only if the field is present, and avoid failing tests for optional fields that are legitimately absent.

---

# Q59. What validations are commonly forgotten?

- Incorrect data types
- Null values
- Empty arrays
- Duplicate records
- Unexpected fields
- Invalid date formats
- Decimal precision
- Business constraints

---

# Q60. How would you improve API validation in a large enterprise?

## Strong Interview Answer

I would implement reusable validation utilities, adopt Pydantic models for strongly typed responses, validate contracts using JSON Schema or OpenAPI specifications, centralize business rule validation, and integrate response validation into CI/CD pipelines. This approach reduces duplication, improves maintainability, and ensures consistent validation across all services.

---

# Architect's Notes

## Problem

Every test repeats the same assertions.

```python
assert response.status_code == 200

assert response.headers["Content-Type"] == "application/json"

assert response.elapsed.total_seconds() < 2
```

Across hundreds of tests, this becomes difficult to maintain.

---

## Better Design

```text
tests/

↓

ResponseValidator

↓

StatusValidator

↓

SchemaValidator

↓

BusinessValidator

↓

PerformanceValidator
```

Tests become:

```python
ResponseValidator.validate_success(response)

UserValidator.validate_user(response.json())
```

Benefits:

- Reusable
- Consistent
- Easy to extend
- Centralized validation logic

---

# Quick Revision

Remember these concepts:

- Status Validation
- Header Validation
- JSON Validation
- Nested Objects
- Arrays
- Required Fields
- Optional Fields
- JSON Schema
- Pydantic
- Business Rules
- Response Time
- Contract Validation
- ResponseValidator
- SchemaValidator
- PerformanceValidator
