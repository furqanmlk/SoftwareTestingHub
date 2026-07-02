## Part 01 – API Fundamentals & REST Concepts

---

# Table of Contents

1. What is an API?
2. Why APIs Matter
3. API Architecture
4. REST Architecture
5. REST Constraints
6. HTTP Request Structure
7. HTTP Response Structure
8. HTTP Methods
9. Status Codes
10. Headers
11. Path Parameters
12. Query Parameters
13. JSON Fundamentals
14. Idempotency
15. Safe vs Unsafe HTTP Methods
16. API Testing Best Practices
17. Interview Questions (Q1-Q15)

---

# What is an API?

## Definition

API stands for **Application Programming Interface**.

An API is a contract that allows two software systems to communicate with each other using predefined requests and responses.

Think of an API as a waiter in a restaurant.

```text
Customer

↓

Waiter (API)

↓

Kitchen (Server)

↓

Waiter

↓

Customer
```

The customer never enters the kitchen.

Similarly, the client application never accesses the database directly.

---

# Real World Example

Imagine an online shopping application.

```text
Browser

↓

GET /products

↓

Product Service

↓

Database

↓

JSON Response

↓

Browser
```

The browser does not communicate directly with the database.

It communicates through APIs.

---

# Why APIs Matter

Modern applications are built using APIs.

Examples

```text
Mobile App

↓

REST API

↓

Database
```

```text
Website

↓

REST API

↓

Authentication Service
```

```text
Frontend

↓

REST API

↓

Payment Service
```

---

# Why Test APIs?

API testing provides several advantages over UI testing.

| API Testing | UI Testing |
|-------------|------------|
| Faster | Slower |
| Stable | More UI changes |
| Easier Debugging | More Difficult |
| Independent of UI | Depends on UI |
| Excellent for CI/CD | Higher execution cost |

---

# API Architecture

```text
Client

↓

HTTP Request

↓

API Server

↓

Business Logic

↓

Database

↓

HTTP Response

↓

Client
```

---

# Types of APIs

| Type | Description |
|------|-------------|
| REST | Most common web API |
| SOAP | XML-based enterprise API |
| GraphQL | Client specifies required data |
| gRPC | High-performance RPC framework |
| WebSocket | Real-time bidirectional communication |

---

# REST Architecture

REST stands for

**Representational State Transfer**

REST is an architectural style for designing web services.

A REST API exposes resources using URLs.

Example

```text
/users

/products

/orders

/payments
```

Resources are manipulated using HTTP methods.

---

# REST Constraints

A RESTful API follows six constraints.

## 1. Client-Server

Client and server are independent.

---

## 2. Stateless

Each request contains all required information.

The server does not remember previous requests.

Example

Every request includes:

- Authentication
- Parameters
- Headers

---

## 3. Cacheable

Responses can be cached.

Benefits

- Faster performance
- Reduced server load

---

## 4. Uniform Interface

Resources follow predictable URLs.

Example

```text
GET /users

POST /users

GET /users/123

DELETE /users/123
```

---

## 5. Layered System

Requests may pass through:

- Gateway
- Load Balancer
- Firewall
- Authentication Service

without the client knowing.

---

## 6. Code on Demand (Optional)

Server may return executable code.

Rarely used today.

---

# HTTP Request Structure

```text
POST /users HTTP/1.1

Host: api.company.com

Authorization: Bearer Token

Content-Type: application/json

Body

{

"name":"John"

}
```

---

# Request Components

| Component | Purpose |
|------------|----------|
| URL | API endpoint |
| Method | GET, POST, etc. |
| Headers | Metadata |
| Query Parameters | Filtering |
| Path Parameters | Resource identification |
| Body | Data payload |

---

# HTTP Response Structure

```text
HTTP/1.1 200 OK

Content-Type: application/json

Body

{

"id":101,

"name":"John"

}
```

---

# Response Components

| Component | Description |
|------------|-------------|
| Status Code | Result |
| Headers | Metadata |
| Body | Returned data |

---

# HTTP Methods

---

## GET

Retrieve data.

Example

```http
GET /users
```

Python Example

```python
import requests

response = requests.get(
    "https://api.company.com/users"
)
```

Characteristics

- Read only
- Safe
- Idempotent

---

## POST

Create new resources.

```http
POST /users
```

Python

```python
requests.post(
    url,
    json=data
)
```

---

## PUT

Replace an existing resource.

```http
PUT /users/5
```

PUT replaces the complete object.

---

## PATCH

Update only selected fields.

Example

```json
{

"email":"new@email.com"

}
```

---

## DELETE

Delete a resource.

```http
DELETE /users/5
```

---

# HTTP Status Codes

## 2xx Success

| Code | Meaning |
|------|----------|
|200|OK|
|201|Created|
|202|Accepted|
|204|No Content|

---

## 3xx Redirection

| Code | Meaning |
|------|----------|
|301|Moved Permanently|
|302|Found|
|304|Not Modified|

---

## 4xx Client Errors

| Code | Meaning |
|------|----------|
|400|Bad Request|
|401|Unauthorized|
|403|Forbidden|
|404|Not Found|
|405|Method Not Allowed|
|409|Conflict|
|422|Validation Error|
|429|Too Many Requests|

---

## 5xx Server Errors

| Code | Meaning |
|------|----------|
|500|Internal Server Error|
|502|Bad Gateway|
|503|Service Unavailable|
|504|Gateway Timeout|

---

# Headers

Headers provide metadata.

Common headers

```text
Authorization

Content-Type

Accept

User-Agent

Cache-Control

If-Match

Correlation-ID
```

Python

```python
headers = {

"Authorization": "Bearer TOKEN",

"Accept": "application/json"

}
```

---

# Path Parameters

Path parameters identify a resource.

Example

```text
/users/100
```

100 is the path parameter.

Python

```python
user_id = 100

url = f"/users/{user_id}"
```

---

# Query Parameters

Query parameters filter or search.

Example

```text
/users?page=2

/users?status=active

/users?sort=name
```

Python

```python
params = {

"page":2,

"status":"active"

}

requests.get(
    url,
    params=params
)
```

---

# JSON Fundamentals

Most REST APIs exchange JSON.

Example

```json
{

"id":1,

"name":"John",

"email":"john@email.com",

"active":true

}
```

Common JSON Types

| Type | Example |
|------|---------|
|String|"John"|
|Number|100|
|Boolean|true|
|Object|{}|
|Array|[]|
|Null|null|

---

# Idempotency

## Definition

An operation is idempotent if performing it multiple times produces the same final result.

---

Examples

GET

```text
GET /users/5

GET /users/5

GET /users/5
```

Same result.

---

DELETE

```text
DELETE /users/5
```

Repeated DELETE requests leave the resource deleted.

---

POST

```text
POST /users
```

Usually NOT idempotent.

Each request creates a new resource.

---

# Safe vs Unsafe Methods

| Method | Safe | Idempotent |
|---------|------|------------|
|GET|Yes|Yes|
|HEAD|Yes|Yes|
|OPTIONS|Yes|Yes|
|PUT|No|Yes|
|DELETE|No|Yes|
|PATCH|No|Usually No|
|POST|No|No|

---

# API Testing Best Practices

✔ Validate status code

✔ Validate response body

✔ Validate response headers

✔ Validate response time

✔ Validate schema

✔ Validate error messages

✔ Test positive scenarios

✔ Test negative scenarios

✔ Test edge cases

✔ Automate repeatable tests

---

# Interview Questions

---

# Q1. What is an API?

## Short Interview Answer

An API is a contract that enables different software applications to communicate using requests and responses.

---

## Senior Interview Answer

An API defines how clients interact with backend services. It abstracts business logic and data access behind a consistent interface, enabling independent development, testing, and deployment of applications.

---

## Real Project Example

In an e-commerce platform, the frontend retrieves product information by calling `GET /products`. The API processes the request, queries the database, and returns a JSON response.

---

# Q2. Why is API Testing important?

## Short Interview Answer

API testing validates business logic before the user interface, providing faster and more reliable feedback.

---

## Senior Interview Answer

API tests are typically more stable than UI tests because they are not affected by UI layout changes. They execute quickly, integrate well with CI/CD pipelines, and allow defects to be detected earlier in the development lifecycle.

---

# Q3. REST vs SOAP?

| REST | SOAP |
|------|------|
|JSON|XML|
|Lightweight|Heavier|
|HTTP|Multiple protocols|
|Fast|More verbose|
|Stateless|Can be stateful|

---

# Q4. Explain HTTP Methods.

Expected Answer

- GET retrieves data.
- POST creates new resources.
- PUT replaces an existing resource.
- PATCH partially updates a resource.
- DELETE removes a resource.

---

# Q5. What is Statelessness?

Each request contains all required information.

The server does not store session information between requests.

---

# Q6. Difference between Path and Query Parameters?

Path Parameter

```text
/users/10
```

Query Parameter

```text
/users?page=2
```

---

# Q7. What is Idempotency?

An idempotent operation produces the same result even when executed multiple times.

---

# Q8. Why is POST not idempotent?

Each POST request typically creates a new resource, so multiple identical requests can produce multiple resources.

---

# Q9. Which HTTP methods are idempotent?

- GET
- PUT
- DELETE
- HEAD
- OPTIONS

---

# Q10. What is JSON?

JSON (JavaScript Object Notation) is a lightweight, human-readable data format commonly used for API communication.

---

# Q11. What should every API test validate?

- Status code
- Response body
- Headers
- Response time
- Schema
- Business rules

---

# Q12. Why are APIs preferred over UI tests in CI/CD?

Because API tests execute faster, are less brittle, and provide earlier feedback on business logic without relying on the user interface.

---

# Q13. What are common API status codes?

- 200 OK
- 201 Created
- 204 No Content
- 400 Bad Request
- 401 Unauthorized
- 403 Forbidden
- 404 Not Found
- 500 Internal Server Error

---

# Q14. What makes an API RESTful?

A RESTful API follows REST constraints, exposes resources through predictable URLs, uses standard HTTP methods, remains stateless, and returns standard HTTP status codes.

---

# Q15. How would you test an API endpoint?

## Strong Interview Answer

I begin by understanding the API contract and expected behavior. I validate the HTTP status code, response body, headers, schema, and response time. I then execute positive, negative, boundary, authorization, and error-handling scenarios. Finally, I automate the tests using Python and Pytest and integrate them into the CI/CD pipeline.

---

# Quick Revision

Remember these keywords:

- API
- REST
- Resource
- Endpoint
- Request
- Response
- Headers
- JSON
- Status Codes
- GET
- POST
- PUT
- PATCH
- DELETE
- Idempotency
- Stateless
- Query Parameters
- Path Parameters
