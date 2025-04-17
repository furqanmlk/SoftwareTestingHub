### 🔐 Security Testing for Login, Encryption, and Session Handling

**Scenario:** Testing the login and session management for a **banking web application**.

I performed the following manual tests to validate the security of authentication, session handling, and sensitive data protection:

| 🧪 Test Type                      | 💡 Example Scenario                                                                 |
|----------------------------------|-------------------------------------------------------------------------------------|
| **1. Input Validation (Login)**  | Entered `' OR 1=1 --` in the username field to check for SQL injection prevention. |
| **2. Brute-force Protection**    | Repeated failed logins to verify lockout or CAPTCHA activation after X attempts.   |
| **3. Session Management**        | Copied the session cookie, logged out, and reused the cookie – ensured session was invalidated. |
| **4. Insecure Direct Access**    | Tried accessing `/dashboard` URL without login – app redirected to login page.     |
| **5. Password Handling**         | Checked if password fields were masked and reset links expired correctly.          |
| **6. Token Expiry & Refresh**    | Let session idle to test JWT expiration and verified token refresh behavior.       |
| **7. Encryption Verification**   | Verified tokens/credentials are not in localStorage or passed via URL parameters.  |
| **8. Role-Based Access Control** | Logged in as a regular user and accessed admin routes – received 403 Forbidden.    |

**🔧 Issue Found:**  
Session token wasn’t invalidated upon logout, allowing reuse via browser tab. Reported as a **critical bug**. Dev team fixed it by implementing **server-side session revocation**.

**✅ Result:**  
Helped prevent potential session hijacking and ensured secure logout behavior, significantly enhancing user data protection.
