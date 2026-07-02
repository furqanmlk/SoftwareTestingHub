## Part 03 – API Authentication (OAuth2, JWT, API Keys & Enterprise Security)

---

# Table of Contents

1. Why Authentication Matters
2. Authentication vs Authorization
3. Common Authentication Methods
4. Basic Authentication
5. API Key Authentication
6. Bearer Token Authentication
7. JWT Authentication
8. OAuth 2.0
9. Refresh Tokens
10. Token Expiration
11. Secure Token Management
12. Authentication Framework Design
13. Interview Questions (Q31–Q45)

---

# Why Authentication Matters

Most enterprise APIs are protected.

Without authentication:

```text
Client

↓

GET /users

↓

401 Unauthorized
```

With authentication:

```text
Client

↓

Access Token

↓

API

↓

200 OK
```

Authentication ensures only authorized users and systems can access protected resources.

---

# Authentication vs Authorization

Many interviewers ask this first.

## Authentication

Authentication answers:

> **Who are you?**

Examples:

- Username & Password
- API Key
- JWT
- OAuth Token

---

## Authorization

Authorization answers:

> **What are you allowed to do?**

Example

```text
Admin

↓

Create User

Delete User

Update User

View Reports
```

Regular User

```text
View Profile

Update Profile
```

---

# Authentication Flow

```text
Client

↓

Login Request

↓

Authentication Server

↓

Access Token

↓

API Request

↓

Protected Resource
```

---

# Common Authentication Methods

| Method | Enterprise Usage |
|----------|----------------|
| Basic Authentication | Legacy Systems |
| API Keys | Public APIs |
| Bearer Token | REST APIs |
| JWT | Microservices |
| OAuth2 | Enterprise Applications |
| Mutual TLS | Banking / Healthcare |

---

# Basic Authentication

Basic Authentication sends:

```text
username:password
```

encoded in Base64.

Header

```http
Authorization: Basic dXNlcjpwYXNzd29yZA==
```

Python

```python
import requests

response = requests.get(

    url,

    auth=("username", "password")

)
```

---

## Limitations

- Credentials sent with every request
- Must always use HTTPS
- Limited scalability

---

# API Key Authentication

Some APIs use API Keys.

Example

```http
x-api-key: abc123xyz
```

Python

```python
headers = {

    "x-api-key": API_KEY

}

response = requests.get(

    url,

    headers=headers

)
```

---

## Best Practices

Never hardcode API keys.

Use:

- Environment Variables
- GitHub Secrets
- Azure Key Vault
- AWS Secrets Manager

---

# Bearer Token Authentication

Most enterprise REST APIs use Bearer Tokens.

Header

```http
Authorization: Bearer eyJhbGciOi...
```

Python

```python
headers = {

    "Authorization":

    f"Bearer {token}"

}

response = requests.get(

    url,

    headers=headers

)
```

---

# JWT (JSON Web Token)

JWT is one of the most common authentication mechanisms.

Structure

```text
Header

.

Payload

.

Signature
```

Example

```text
xxxxx.yyyyy.zzzzz
```

---

# JWT Payload

Example

```json
{

"userId":101,

"role":"Admin",

"exp":1735689600

}
```

Contains:

- User ID
- Roles
- Permissions
- Expiration

---

# JWT Workflow

```text
Login

↓

Server

↓

JWT

↓

Client Stores Token

↓

API Request

↓

Authorization Header

↓

Protected Endpoint
```

---

# Why JWT?

Advantages

- Stateless
- Lightweight
- Scalable
- Easy for Microservices
- No server-side session storage

---

# OAuth 2.0

OAuth is an authorization framework.

Instead of sharing passwords,

users grant limited access.

---

## OAuth Example

```text
User

↓

Login with Google

↓

Google

↓

Access Token

↓

Application
```

---

## OAuth Roles

| Role | Description |
|------|-------------|
| Resource Owner | User |
| Client | Application |
| Authorization Server | Issues Tokens |
| Resource Server | Protected API |

---

# OAuth Flow (Authorization Code)

```text
User

↓

Application

↓

Authorization Server

↓

Login

↓

Authorization Code

↓

Application

↓

Access Token

↓

API
```

---

# Refresh Tokens

Access Tokens expire.

Instead of asking the user to login again:

```text
Expired Access Token

↓

Refresh Token

↓

New Access Token
```

---

# Why Refresh Tokens?

Benefits

- Better user experience
- Improved security
- Short-lived access tokens

---

# Token Expiration

Always validate:

- Expired Token
- Invalid Token
- Revoked Token
- Missing Token

Expected Responses

```text
401 Unauthorized

403 Forbidden
```

---

# Secure Token Storage

Never store tokens:

❌ Source Code

❌ Git Repository

❌ Plain Text Files

Use

✔ GitHub Secrets

✔ Environment Variables

✔ Secret Manager

---

# Environment Variables

Example

```python
import os

TOKEN = os.getenv("API_TOKEN")
```

---

# Authentication Framework Design

Enterprise API frameworks usually separate authentication.

Example

```text
api/

├── auth_client.py

├── users_client.py

├── products_client.py

├── orders_client.py
```

---

## Authentication Client

Example

```python
class AuthClient:

    def login(self):

        ...

    def refresh_token(self):

        ...

    def logout(self):

        ...
```

Other clients use:

```python
auth.token
```

instead of logging in repeatedly.

---

# Automatic Token Refresh

Good frameworks automatically refresh tokens.

```text
Request

↓

401 Unauthorized

↓

Refresh Token

↓

Retry Request

↓

200 OK
```

This should be transparent to test cases.

---

# Common Authentication Test Scenarios

Positive

- Valid credentials
- Valid token
- Valid API key

Negative

- Invalid password
- Invalid token
- Expired token
- Missing token
- Revoked token

Security

- Token tampering
- Token replay
- Expired refresh token
- Unauthorized role

---

# Interview Questions

---

# Q31. Authentication vs Authorization?

## Short Interview Answer

Authentication verifies identity.

Authorization determines permissions.

---

## Example

Authentication

Who are you?

Authorization

What can you do?

---

# Q32. What is JWT?

## Short Interview Answer

JWT is a stateless authentication token consisting of a header, payload, and signature.

---

## Senior Interview Answer

JWT allows authentication information to travel with each request without requiring the server to maintain session state. This makes it highly scalable for distributed systems and microservices.

---

# Q33. Why is JWT popular in Microservices?

## Answer

Because each service can validate the token independently.

Benefits

- Stateless
- Scalable
- Distributed
- Fast

---

# Q34. Why shouldn't JWT contain sensitive information?

Although JWTs are signed, their payload is only Base64 encoded—not encrypted. Anyone who obtains the token can decode and read its contents.

Sensitive data such as passwords or credit card numbers should never be stored in a JWT payload.

---

# Q35. What is OAuth?

OAuth is an authorization framework that allows users to grant applications limited access without sharing their credentials.

---

# Q36. Why use Refresh Tokens?

Refresh Tokens allow clients to obtain new access tokens after expiration without requiring the user to authenticate again.

---

# Q37. Where should tokens be stored?

Use:

- Environment Variables
- Secret Managers
- CI/CD Secrets

Avoid:

- Source Code
- Git Repositories
- Configuration Files committed to version control

---

# Q38. How do you test authentication?

I validate:

- Valid credentials
- Invalid credentials
- Missing credentials
- Expired tokens
- Invalid signatures
- Unauthorized roles
- Refresh token flow

---

# Q39. What HTTP status codes are common for authentication?

| Code | Meaning |
|------|----------|
|200|Success|
|201|Created|
|400|Bad Request|
|401|Unauthorized|
|403|Forbidden|

---

# Q40. API Key vs JWT?

| API Key | JWT |
|----------|-----|
|Simple|More Secure|
|Static|Temporary|
|Limited Identity|Contains Claims|
|Good for Service APIs|Good for User Authentication|

---

# Q41. Why use HTTPS with authentication?

HTTPS encrypts data in transit, preventing attackers from intercepting credentials or access tokens.

---

# Q42. How would you design authentication in an API framework?

## Strong Interview Answer

I would centralize authentication in a dedicated `AuthClient` responsible for login, token refresh, and logout. Tokens would be cached in memory during test execution, refreshed automatically when expired, and injected into API clients through dependency injection. Credentials and secrets would be stored securely using environment variables or CI/CD secret managers.

---

# Q43. What should happen if a token expires during a test?

The framework should:

1. Detect the `401 Unauthorized` response.
2. Request a new access token using the refresh token.
3. Retry the original request automatically.
4. Report the failure only if re-authentication is unsuccessful.

---

# Q44. What authentication scenarios are commonly forgotten?

- Expired tokens
- Revoked tokens
- Missing scopes
- Invalid audience (`aud`)
- Invalid issuer (`iss`)
- Clock skew
- Multiple simultaneous logins
- Token reuse after logout

---

# Q45. How do you secure API automation in CI/CD?

## Strong Interview Answer

I never store credentials or tokens in source code. Secrets are managed through GitHub Secrets or a cloud secret manager. Access tokens are generated at runtime, rotated regularly, and never written to logs or reports. Sensitive values are masked during execution, and least-privilege access is enforced for automation accounts.

---

# Architect's Notes

## Problem

Every API client performs its own login.

```python
def get_user():
    login()
    requests.get(...)
```

Problems:

- Slow execution
- Duplicate code
- Difficult maintenance
- Excessive authentication requests

---

## Recommended Solution

Centralize authentication.

```text
AuthClient

↓

Access Token

↓

UsersClient

OrdersClient

ProductsClient

PaymentsClient
```

Benefits

- One authentication flow
- Automatic token refresh
- Faster execution
- Easier maintenance
- Consistent security

---

# Quick Revision

Remember these concepts:

- Authentication
- Authorization
- Basic Authentication
- API Key
- Bearer Token
- JWT
- OAuth2
- Refresh Token
- Access Token
- Token Expiration
- Secret Management
- HTTPS
- AuthClient
- Token Refresh
- Environment Variables
