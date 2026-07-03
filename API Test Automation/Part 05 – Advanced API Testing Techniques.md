## Part 05 – Advanced API Testing Techniques

---

# Table of Contents

1. Positive vs Negative Testing
2. Boundary Value Testing
3. Idempotency Testing
4. Pagination Testing
5. Filtering Testing
6. Sorting Testing
7. Search Testing
8. Partial Updates (PATCH)
9. Error Handling Validation
10. Retry Mechanisms
11. Rate Limiting
12. Eventual Consistency
13. Asynchronous APIs
14. Correlation IDs
15. Advanced Interview Questions (Q61-Q80)

---

# Why Advanced API Testing?

Many automation engineers verify only:

- Status code
- Response body

Senior engineers validate:

- Business workflows
- Edge cases
- Performance
- Security
- Scalability
- Resilience
- Reliability

---

# Positive Testing

Positive tests verify expected behavior using valid inputs.

Example

```text
POST /users

Valid Payload

↓

201 Created
```

Example

```python
payload = {

    "firstName": "John",

    "lastName": "Smith"

}

response = client.create_user(payload)

assert response.status_code == 201
```

---

# Negative Testing

Negative testing verifies the API rejects invalid input correctly.

Example

```text
POST /users

Missing Email

↓

400 Bad Request
```

Validation

```python
assert response.status_code == 400

assert "email" in response.json()["message"]
```

---

# Boundary Value Testing

Many defects occur at boundaries.

Example

Password length

Minimum

8

Maximum

32

Test

- 7
- 8
- 9
- 31
- 32
- 33

---

# Example

Age

Allowed

18–65

Test

17

18

19

64

65

66

---

# Equivalence Partitioning

Instead of testing every value,

divide inputs into valid and invalid groups.

Example

Age

0–17

Invalid

18–65

Valid

66+

Invalid

Choose representative values.

---

# Pagination Testing

Example API

```text
GET /users?page=2&pageSize=20
```

Validate

- Page size
- Total records
- Current page
- Next page
- Previous page
- Empty last page

Example

```python
response = client.get_users(

    page=2,

    page_size=20

)

assert len(response.json()["data"]) <= 20
```

---

# Filtering Testing

Example

```text
/users?status=ACTIVE
```

Validation

Every returned user

↓

Status

↓

ACTIVE

Example

```python
for user in users:

    assert user["status"] == "ACTIVE"
```

---

# Sorting Testing

Example

```text
/users?sort=name
```

Validation

```python
names = [

    u["name"]

    for u in users

]

assert names == sorted(names)
```

Descending

```python
assert names == sorted(

    names,

    reverse=True

)
```

---

# Search Testing

Example

```text
/users?search=John
```

Validate

Every result should match the search criteria.

---

# Partial Update Testing (PATCH)

Original

```json
{

"name":"John",

"email":"john@email.com"

}
```

PATCH

```json
{

"name":"Mike"

}
```

Validation

Name changes

Email remains unchanged

---

# DELETE Validation

After

```text
DELETE /users/5
```

Validate

```text
GET /users/5

↓

404 Not Found
```

---

# Duplicate Resource Testing

Example

Create

```
john@email.com
```

Create again

```
john@email.com
```

Expected

```text
409 Conflict
```

---

# Retry Mechanisms

Cloud services occasionally fail.

Example

```text
500

↓

Retry

↓

200
```

Retry only for transient failures.

Do NOT retry

- Validation errors
- Authentication failures
- Authorization failures

---

# Exponential Backoff

Instead of

```text
1

1

1

1
```

Use

```text
1 second

2 seconds

4 seconds

8 seconds
```

This reduces server load.

---

# Rate Limiting

Many APIs restrict request rates.

Example

```
100 requests/minute
```

Expected

```
429 Too Many Requests
```

Validate

- Retry-After header
- Proper status code
- Recovery after waiting

---

# Correlation ID

Enterprise APIs usually include

```text
X-Correlation-ID
```

Purpose

Track a request across multiple services.

Validation

```python
assert "X-Correlation-ID" in response.headers
```

---

# Eventual Consistency

Microservices may not update immediately.

Example

```text
POST /orders

↓

Order Queue

↓

Inventory

↓

Notification

↓

Database
```

The response may be successful before all downstream systems have updated.

Testing strategy:

- Poll with timeout
- Verify final state
- Avoid fixed delays

---

# Asynchronous APIs

Some APIs return

```
202 Accepted
```

instead of

```
200 OK
```

Flow

```text
Submit Request

↓

202 Accepted

↓

Processing

↓

Status Endpoint

↓

Completed
```

Testing requires polling until completion.

---

# Polling Example

```python
import time

for _ in range(10):

    response = client.get_job(job_id)

    if response.json()["status"] == "Completed":
        break

    time.sleep(2)

assert response.json()["status"] == "Completed"
```

---

# Advanced Validation Checklist

Every enterprise API should be tested for:

✓ Status Code

✓ Response Body

✓ Headers

✓ Schema

✓ Performance

✓ Pagination

✓ Filtering

✓ Sorting

✓ Search

✓ Authorization

✓ Error Messages

✓ Idempotency

✓ Rate Limiting

✓ Retry Behavior

✓ Eventual Consistency

---

# Interview Questions

---

# Q61. How do you test pagination?

## Short Interview Answer

Validate page size, page number, total records, navigation between pages, and empty page behavior.

---

## Senior Interview Answer

I verify pagination metadata, ensure no duplicate or missing records across pages, validate boundary pages (first and last), and confirm consistent ordering when navigating through results.

---

# Q62. How do you test filtering?

Validate that every returned record satisfies the filter criteria.

---

# Q63. How do you test sorting?

Verify ascending and descending ordering, including duplicate values and null handling.

---

# Q64. How do you test search functionality?

Validate exact matches, partial matches, case sensitivity (if applicable), special characters, and empty results.

---

# Q65. How do you test PATCH requests?

Verify that only the specified fields change while all other fields remain unchanged.

---

# Q66. What is eventual consistency?

Eventual consistency means distributed systems may require time before all services reflect the latest data. Tests should poll for the expected state rather than assuming immediate consistency.

---

# Q67. How do you test asynchronous APIs?

Validate the initial `202 Accepted` response, poll the status endpoint until completion or timeout, and then verify the final result.

---

# Q68. What is rate limiting?

Rate limiting restricts how many requests a client can make within a given period. Tests should verify `429 Too Many Requests`, `Retry-After` headers, and successful recovery.

---

# Q69. When should retries be used?

Retries should only handle transient failures such as temporary network issues, timeouts, or brief server unavailability. They should not hide genuine application defects.

---

# Q70. How do you test duplicate data?

Submit the same request twice and verify that the API either rejects duplicates appropriately (for example, `409 Conflict`) or behaves according to the documented business rules.

---

# Q71. What negative scenarios do you automate?

- Missing required fields
- Invalid data types
- Invalid authentication
- Unauthorized access
- Invalid path parameters
- Invalid query parameters
- Duplicate resources
- Expired tokens
- Invalid JSON
- Unsupported media types

---

# Q72. How do you validate idempotency?

Execute the same idempotent request multiple times and verify that the final system state remains unchanged.

---

# Q73. Why is the Correlation ID important?

Correlation IDs allow engineers to trace a request across multiple services, making debugging significantly easier in distributed systems.

---

# Q74. How do you validate retry behavior?

Simulate transient failures, confirm retries occur according to policy, and ensure the request eventually succeeds or fails gracefully after the configured retry limit.

---

# Q75. How would you improve API test coverage?

## Strong Interview Answer

I would combine positive, negative, boundary, security, authorization, pagination, filtering, sorting, performance, and contract tests. I would also include edge cases, asynchronous workflows, and resilience testing to provide comprehensive coverage.

---

# Architect's Notes

## Problem

Teams often validate only successful responses.

```text
200 OK

↓

Pass
```

This leaves many defects undiscovered.

---

## Better Strategy

```text
Positive Tests

↓

Negative Tests

↓

Boundary Tests

↓

Security Tests

↓

Performance Tests

↓

Resilience Tests

↓

Contract Tests
```

A mature API automation suite validates not only **correctness**, but also **robustness** under realistic conditions.

---

# Quick Revision

Remember these concepts:

- Positive Testing
- Negative Testing
- Boundary Values
- Equivalence Partitioning
- Pagination
- Filtering
- Sorting
- Search
- PATCH
- Retry
- Exponential Backoff
- Rate Limiting
- Correlation ID
- Eventual Consistency
- Asynchronous APIs
- Polling
