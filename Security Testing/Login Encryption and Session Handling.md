### 🔐 Security Testing for Login, Encryption, and Session Handling

## 🛠️ How to Perform Common Security Tests for Login, Tokens, and Sessions

| 🧪 Test | 🔍 How to Perform It |
|--------|-----------------------|
| **1. Input Validation (Login)** | Enter payloads like `' OR 1=1 --` or `<script>alert(1)</script>` in the login fields. Ensure no SQL errors or XSS behavior is observed. |
| **2. Brute-force Protection** | Attempt invalid logins multiple times. Keycloak should lock the account or trigger CAPTCHA after a set number of failures. |
| **3. Session Management (Reuse Token)** | 1. Login and copy access token from browser dev tools or Postman. <br> 2. Logout. <br> 3. Reuse token in Postman or browser. Expected: token is invalidated and request is rejected. |
| **4. Token Expiry & Refresh** | 1. Wait for the token to expire (`expires_in`). <br> 2. Try accessing protected API or route. <br> 3. App should attempt refresh token or force login. |
| **5. SSO / Single Logout (SLO)** | 1. Login to App A. <br> 2. Access App B (auto-login via SSO). <br> 3. Logout from App A. <br> 4. Refresh App B. Expected: also logged out. |
| **6. Role-Based Access Control (RBAC)** | Login as a low-privileged user (e.g., "user" role) and attempt to access admin-only routes or APIs. Expected: access denied (403). |
| **7. Insecure Direct Access** | Copy a protected route URL. Open it in Incognito without logging in. Expected: redirected to Keycloak login. |
| **8. Token Inspection (JWT)** | Copy access token and paste in [https://jwt.io](https://jwt.io). Confirm token does not expose sensitive data like passwords or PII. |
| **9. Token Manipulation** | Slightly modify a valid token (e.g., change 1 character) and reuse it in a request. Expected: server should reject with 401. |
| **10. PKCE Flow (for mobile apps)** | Use a proxy tool (Charles/Fiddler) to inspect OAuth flow. Check `code_challenge` and `code_verifier` consistency and behavior. |
| **11. Logout Redirect Validation** | During logout, test with a modified `post_logout_redirect_uri` pointing to an external site. Expected: Keycloak should reject invalid URIs not whitelisted in the client config. |

---

## 🧰 Useful Tools

| Tool | Purpose |
|------|---------|
| **Browser Dev Tools** | Inspect tokens, session, and network activity |
| **Postman** | Manually test API authentication flows |
| **JWT.io** | Decode and inspect JWTs for structure and payload |
| **Burp Suite / OWASP ZAP** | Perform advanced security fuzzing and penetration testing |
| **Charles Proxy / Fiddler** | Intercept and analyze mobile and web OAuth flows |

---

## ✅ Tips

- Always **test with different user roles** (admin, user, guest).
- Document token lifecycles, refresh logic, and logout behavior.
- Validate Keycloak client settings for **redirect URIs**, **role mappers**, and **token expiration settings**.


