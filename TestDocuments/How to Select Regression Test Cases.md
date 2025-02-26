# **How to Select Test Cases for Regression Testing from Functional Testing?**

## **📌 What is Regression Testing?**
Regression Testing ensures that **new changes or bug fixes do not break existing functionality**. Instead of re-executing **all** functional test cases, **a subset** is selected for efficient testing.

---

## **📌 Steps to Select Test Cases for Regression Testing**
### **1️⃣ Identify Business-Critical Features**
- Prioritize test cases that cover the **core functionalities** of the application.
- Example: In an **eCommerce website**, selecting test cases for:
  - ✅ **User login/logout**
  - ✅ **Product search and filtering**
  - ✅ **Cart and checkout flow**
  - ✅ **Order placement and payment processing**

---

### **2️⃣ Analyze Areas Affected by Code Changes**
- Review **what has changed** in the latest release (new features, bug fixes, refactoring).
- Identify **dependent modules** that could be affected.
- Example: If **"Apply Discount Coupon"** logic is updated, select test cases for:
  - ✅ Discount calculations.
  - ✅ Cart updates after applying/removing coupons.
  - ✅ Price breakdown on checkout.

---

### **3️⃣ Select High-Risk and High-Impact Test Cases**
- Choose test cases that cover **frequently used functionalities**.
- Select **complex workflows** or **integration test cases** that involve multiple modules.
- Example: A **multi-step checkout process** involving:
  - 🛒 Adding an item to the cart.
  - 🚚 Selecting a shipping address.
  - 💳 Applying a discount code.
  - ✅ Processing payment.

---

### **4️⃣ Include Test Cases for Recent Bug Fixes**
- Select test cases that verify **recently fixed defects** to prevent **regressions**.
- Example: If a bug in the **password reset feature** was fixed, include:
  - ✅ A test for resetting passwords via email.
  - ✅ A test for invalid password reset attempts.

---

### **5️⃣ Cover Cross-Module and Integration Scenarios**
- Ensure **data flow** between modules works correctly.
- Example: A **user profile update** should reflect:
  - ✅ In the **user account section**.
  - ✅ In the **order history**.
  - ✅ In the **customer service portal**.

---

### **6️⃣ Consider Test Case Execution History**
- Prioritize **previously failed test cases**, as they have a higher probability of failing again.
- Select **frequently failing** or **flaky test cases**.

---

### **7️⃣ Include Performance and Security Regression Tests (if applicable)**
- If performance/security tests exist, **include them in regression testing** for major releases.
- Example: If a **database query was optimized**, test **page load time** for affected screens.

---

### **8️⃣ Balance Between Manual and Automated Tests**
- Prefer **automated test cases** for **faster execution**.
- Select **manual test cases** for **new changes** or **complex workflows**.

---

## **🎯 Types of Test Cases to Include in Regression Testing**
| **Category** | **Example Test Cases** |
|-------------|------------------------|
| **Core Functional Test Cases** | Login, Cart, Checkout, Payment |
| **Recently Fixed Defects** | Password Reset, Order Cancellation Fix |
| **Integration Scenarios** | Order status updates in Admin Panel |
| **Frequently Failing Tests** | Flaky UI or API tests |
| **High-Risk Test Cases** | Multi-step checkout, Data migrations |
| **Performance/Load Test Cases** | API response time, Page load speed |

---

## **📌 Best Practices**
✅ **Prioritize test cases** based on risk and impact.  
✅ **Use test automation** for regression whenever possible.  
✅ **Review test cases regularly** to update/remove outdated ones.  
✅ **Leverage CI/CD pipelines** for continuous regression testing.  

