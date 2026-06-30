## Part 02 – Python API Automation using Requests & HTTPX

---

# Table of Contents

1. Why Python for API Testing
2. Requests vs HTTPX
3. Installing Dependencies
4. Sending HTTP Requests
5. GET Requests
6. POST Requests
7. PUT Requests
8. PATCH Requests
9. DELETE Requests
10. Sending Headers
11. Query Parameters
12. Request Body
13. File Upload
14. Handling Responses
15. Error Handling
16. Timeouts
17. Sessions
18. Retry Strategy
19. Best Practices
20. Interview Questions (Q16–Q30)

---

# Why Python for API Testing?

Python is one of the most popular languages for API automation because it is:

- Easy to read
- Lightweight
- Excellent HTTP libraries
- Great Pytest integration
- Perfect for CI/CD
- AI-friendly

---

# Popular Python Libraries

| Library | Purpose |
|----------|---------|
| requests | REST API Testing |
| HTTPX | Modern HTTP Client |
| pytest | Test Framework |
| Pydantic | Data Validation |
| Faker | Test Data |
| jsonschema | Schema Validation |
| Allure | Reporting |

---

# Requests vs HTTPX

| Feature | Requests | HTTPX |
|----------|-----------|---------|
| Simple API | ✅ | ✅ |
| Async Support | ❌ | ✅ |
| HTTP/2 | ❌ | ✅ |
| Connection Pooling | ✅ | ✅ |
| Timeout Support | ✅ | ✅ |
| Production Ready | ✅ | ✅ |

---

# Which One Should You Learn?

For interviews:

Learn **Requests first** because almost every company uses it.

Learn **HTTPX** because modern applications increasingly use asynchronous APIs.

---

# Installation

```bash
pip install requests
```

```bash
pip install httpx
```

---

# Your First GET Request

```python
import requests

response = requests.get(
    "https://reqres.in/api/users/2"
)

print(response.status_code)
print(response.json())
```

---

# Understanding the Response Object

```python
response.status_code

response.headers

response.text

response.json()

response.elapsed

response.cookies

response.url
```

---

# Validating Status Code

```python
assert response.status_code == 200
```

---

# Validating JSON

```python
data = response.json()

assert data["data"]["id"] == 2
```

---

# POST Request

Suppose we want to create a user.

```python
payload = {

    "name":"John",

    "job":"QA Engineer"

}

response = requests.post(

    "https://reqres.in/api/users",

    json=payload

)

assert response.status_code == 201
```

---

# Why use json= ?

Good

```python
requests.post(

    url,

    json=payload

)
```

Avoid

```python
requests.post(

    url,

    data=json.dumps(payload)

)
```

Using `json=` automatically:

- Converts the dictionary to JSON
- Sets the `Content-Type: application/json` header

---

# PUT Request

Replace an existing resource.

```python
payload = {

    "name":"John",

    "job":"Architect"

}

response = requests.put(

    url,

    json=payload

)
```

---

# PATCH Request

Update only selected fields.

```python
payload = {

    "job":"Lead QA"

}

response = requests.patch(

    url,

    json=payload

)
```

---

# DELETE Request

```python
response = requests.delete(

    url

)

assert response.status_code == 204
```

---

# Sending Headers

```python
headers = {

    "Authorization":

    "Bearer TOKEN",

    "Accept":

    "application/json"

}

response = requests.get(

    url,

    headers=headers

)
```

---

# Query Parameters

Instead of:

```text
/users?page=2
```

Python

```python
params = {

    "page":2

}

response = requests.get(

    url,

    params=params

)
```

Requests automatically creates:

```text
/users?page=2
```

---

# Sending JSON Body

```python
payload = {

    "firstName":"John",

    "lastName":"Smith",

    "email":"john@email.com"

}
```

```python
requests.post(

    url,

    json=payload

)
```

---

# Uploading Files

```python
files = {

    "file": open(

        "report.pdf",

        "rb"

    )

}

requests.post(

    url,

    files=files

)
```

---

# Handling Responses

Example

```python
response = requests.get(url)

print(response.status_code)

print(response.json())

print(response.headers)
```

---

# Common Response Assertions

```python
assert response.status_code == 200

assert response.headers["Content-Type"] == "application/json"

assert response.elapsed.total_seconds() < 2
```

---

# Error Handling

```python
import requests

try:

    response = requests.get(

        url,

        timeout=10

    )

    response.raise_for_status()

except requests.Timeout:

    print("Timeout")

except requests.ConnectionError:

    print("Connection Error")

except requests.HTTPError:

    print("HTTP Error")
```

---

# Why use raise_for_status()?

Instead of manually checking:

```python
if response.status_code != 200:
```

Use

```python
response.raise_for_status()
```

It automatically raises an exception for:

- 400
- 401
- 403
- 404
- 500

---

# Timeouts

Never omit timeouts.

Bad

```python
requests.get(url)
```

Good

```python
requests.get(

    url,

    timeout=30

)
```

---

# Sessions

A Session reuses the TCP connection.

Without Session

```text
Request 1

↓

New Connection

Request 2

↓

New Connection

Request 3

↓

New Connection
```

With Session

```python
session = requests.Session()

session.get(url)

session.post(url)
```

Benefits

- Faster
- Less overhead
- Cookie persistence

---

# Retry Strategy

Network failures happen.

Example

```text
Request

↓

Timeout

↓

Retry

↓

Success
```

Retries should be used only for transient failures.

Avoid retrying:

- Invalid data
- Authentication failures
- Validation errors

---

# HTTPX

Modern Python projects often use HTTPX.

Example

```python
import httpx

response = httpx.get(

    url

)
```

Looks similar to Requests.

---

# Async HTTPX

```python
import httpx
import asyncio

async def get_users():

    async with httpx.AsyncClient() as client:

        response = await client.get(url)

        return response.json()

asyncio.run(

    get_users()

)
```

---

# Why Async?

Useful when:

- Hundreds of API calls
- Performance testing
- Microservices
- Concurrent execution

---

# Requests vs HTTPX Interview Answer

> Requests is excellent for synchronous API automation and is widely used in enterprise environments. HTTPX provides a very similar interface while adding asynchronous support and HTTP/2 capabilities, making it well suited for modern cloud-native applications and high-concurrency testing.

---

# Best Practices

✔ Use Sessions

✔ Always specify timeout

✔ Validate status code

✔ Validate schema

✔ Validate headers

✔ Validate response time

✔ Keep reusable API clients

✔ Never hardcode URLs

✔ Externalize configuration

✔ Use logging

---

# Interview Questions

---

# Q16. Why use Requests for API Testing?

## Short Interview Answer

Requests provides a simple and intuitive API for sending HTTP requests and validating responses.

---

## Senior Interview Answer

Requests is mature, stable, and integrates seamlessly with Pytest. It simplifies API automation by handling HTTP communication, JSON serialization, sessions, and authentication while keeping test code readable.

---

# Q17. What is the Response object?

The Response object contains everything returned by the server.

Examples

```python
response.status_code

response.headers

response.json()

response.text

response.elapsed
```

---

# Q18. Why should you use Sessions?

Sessions reuse TCP connections.

Benefits

- Faster execution
- Cookie persistence
- Reduced network overhead

---

# Q19. Why always specify timeout?

Without a timeout, a request can wait indefinitely if the server does not respond, causing automation pipelines to hang.

---

# Q20. Why use json= instead of data=?

The `json=` parameter automatically serializes Python dictionaries to JSON and sets the appropriate `Content-Type` header.

---

# Q21. How do you validate an API response?

I validate:

- Status code
- Headers
- JSON body
- Business rules
- Schema
- Response time

---

# Q22. What is response.raise_for_status()?

It raises an exception automatically for unsuccessful HTTP responses (4xx and 5xx), allowing failures to be handled consistently.

---

# Q23. Requests vs HTTPX?

| Requests | HTTPX |
|-----------|---------|
| Mature | Modern |
| Sync | Sync + Async |
| HTTP/1 | HTTP/1 + HTTP/2 |
| Widely adopted | Growing rapidly |

---

# Q24. Why use HTTPX?

HTTPX supports asynchronous requests, making it ideal for high-concurrency API testing and modern cloud-native applications.

---

# Q25. Why should API clients be reusable?

Reusable API clients centralize request logic, reduce duplication, and make maintenance easier when endpoints or authentication methods change.

---

# Q26. How would you organize API code?

```text
api/

├── base_client.py

├── users_client.py

├── orders_client.py

├── auth_client.py
```

Each client should encapsulate one domain or service.

---

# Q27. Should API calls be written directly inside tests?

No.

Tests should call reusable API client methods rather than constructing HTTP requests directly.

---

# Q28. How do you improve API automation maintainability?

- Reusable clients
- Centralized configuration
- Common validation utilities
- Logging
- Typed models
- Builder pattern for request payloads

---

# Q29. How do you handle transient network failures?

Retry only for transient issues such as timeouts or temporary server unavailability, using exponential backoff where appropriate.

---

# Q30. How would you build an enterprise API automation framework?

## Strong Interview Answer

I would build reusable API client classes for each business domain, centralize authentication and configuration, externalize environment settings, use Pytest fixtures for dependency injection, validate responses with Pydantic and JSON Schema, generate Allure reports, integrate the framework into GitHub Actions, and design tests to be independent, maintainable, and suitable for parallel execution.

---

# Architect's Notes

## Problem

Different teams duplicate API request logic across hundreds of tests.

---

## Poor Solution

Each test creates its own HTTP requests.

```python
def test_user():
    requests.get(...)
```

This leads to duplication and inconsistent handling of authentication, logging, retries, and validation.

---

## Recommended Solution

Create reusable API client classes.

```python
class UsersClient:

    def get_user(self, user_id):
        ...

    def create_user(self, payload):
        ...

    def delete_user(self, user_id):
        ...
```

Benefits:

- Single source of truth
- Easier maintenance
- Cleaner tests
- Better scalability

---

# Quick Revision

Remember these concepts:

- Requests
- HTTPX
- Sessions
- Response Object
- JSON
- Headers
- Query Parameters
- Timeouts
- Retry Strategy
- API Client
- Async Requests
- Connection Reuse
- Response Validation
