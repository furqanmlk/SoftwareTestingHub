# **Test Case Design Techniques with eCommerce Website Scenario**

## **Scenario: eCommerce Website - Product Purchase Flow**
- A user can purchase products on an eCommerce website.
- The system checks for:
  - User authentication.
  - Item availability in stock.
  - Minimum and maximum order limits.
  - Payment processing.

---

## **1️⃣ Equivalence Partitioning (EP)**
This technique divides input into **valid and invalid partitions** and selects one representative test case from each.

### **Steps to Apply:**
1. Identify input conditions: **Order Quantity**.
2. Divide the input range into partitions:
   - ✅ **Valid Partition:** Order quantity within allowed limits (e.g., 1 to 10 items).
   - ❌ **Invalid Partition 1:** Order quantity below the minimum (e.g., 0 items).
   - ❌ **Invalid Partition 2:** Order quantity above the maximum (e.g., 100 items).
   - ❌ **Invalid Partition 3:** Negative order quantity (e.g., -5 items).

### **Example Test Cases:**
- **Order 5 items** → ✅ Success.
- **Order 0 items** → ❌ Failure (below minimum limit).
- **Order 100 items** → ❌ Failure (above max limit).
- **Order -5 items** → ❌ Failure (negative value not allowed).

---

## **2️⃣ Boundary Value Analysis (BVA)**
This technique tests **values at the boundaries** since errors often occur there.

### **Steps to Apply:**
1. Identify the boundary values (e.g., Min = 1, Max = 10).
2. Test values **just inside and just outside** the boundary.

### **Example Test Cases:**
- **Order 0 items** → ❌ Rejected (just below min limit).
- **Order 1 item** → ✅ Accepted (minimum valid).
- **Order 10 items** → ✅ Accepted (maximum valid).
- **Order 11 items** → ❌ Rejected (just above max limit).

---

## **3️⃣ Error Guessing**
This technique relies on tester experience to predict likely failures.

### **Steps to Apply:**
1. Think of common user errors.
2. Create test cases based on them.

### **Example Test Cases:**
- **Enter a non-numeric order quantity (e.g., "abc")** → ❌ Rejected.
- **Enter special characters in the quantity field (e.g., "#@!")** → ❌ Rejected.
- **Order an item that is out of stock** → ❌ Rejected.
- **Close browser during payment processing** → ❌ Order should not be placed.
- **Use an expired discount coupon** → ❌ Discount should not apply.

---

## **4️⃣ Decision Table Testing**
Used when multiple conditions affect the outcome.

### **Steps to Apply:**
1. Identify input conditions (e.g., Payment Successful, Stock Available, Shipping Address Provided).
2. Create a table covering all combinations.

| **Payment Successful** | **Stock Available** | **Shipping Address Provided** | **Expected Outcome** |
|----------------------|-------------------|-------------------------|------------------|
| ✅ Yes | ✅ Yes | ✅ Yes | ✅ Order Placed Successfully |
| ✅ Yes | ✅ Yes | ❌ No | ❌ Rejected (Address Required) |
| ✅ Yes | ❌ No | ✅ Yes | ❌ Rejected (Out of Stock) |
| ❌ No | ✅ Yes | ✅ Yes | ❌ Rejected (Payment Failed) |

---

## **5️⃣ State Transition Testing**
Used when the system behavior depends on previous states.

### **Steps to Apply:**
1. Identify system states (e.g., User Adds Item → Proceeds to Checkout → Completes Payment).
2. Test transitions between states.

### **Example Test Case:**
1. **User adds item to cart** → **Proceed to checkout** → ✅ Success.
2. **User enters incorrect payment details** → **Payment fails** → ❌ Order not placed.
3. **User corrects payment details** → **Payment succeeds** → ✅ Order placed.
4. **User cancels order before payment** → ❌ Order should not be placed.
5. **User tries to order out-of-stock item** → ❌ System prevents checkout.

---

## **Conclusion**
Each technique provides different insights:
- **Equivalence Partitioning** ensures all input types are tested.
- **Boundary Value Analysis** catches edge cases.
- **Error Guessing** identifies unexpected failures.
- **Decision Table Testing** ensures all rules are applied.
- **State Transition Testing** verifies system flow.
