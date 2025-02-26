# API Testing Techniques
API testing ensures that the **backend functionality** works correctly.

### **Steps to Apply:**
1. Validate **Request and Response** formats.
2. Perform **CRUD operations** (`Create`, `Read`, `Update`, `Delete`).
3. Test with **valid and invalid inputs**.
4. Check **authentication and authorization**.
5. Verify **error handling and status codes**.

---

### **7️⃣ API Methods and Usage**
| **Method** | **Endpoint** | **Purpose** | **Example Request** |
|-----------|------------|------------|------------------|
| **`GET`** | `/products` | Retrieve a list of products. | `GET /products` |
| **`GET`** | `/order/{id}` | Retrieve a specific order. | `GET /order/12345` |
| **`POST`** | `/order` | Create a new order. | `POST /order { "product_id": 101, "quantity": 2 }` |
| **`PUT`** | `/order/{id}` | Update an existing order. | `PUT /order/12345 { "quantity": 3 }` |
| **`DELETE`** | `/order/{id}` | Cancel an order. | `DELETE /order/12345` |
| **`POST`** | `/payment` | Process payment for an order. | `POST /payment { "order_id": 12345, "card_number": "****" }` |

---

### **8️⃣ Example API Test Cases**
| **Test Case** | **API Request** | **Expected Response** |
|--------------|----------------|----------------------|
| ✅ **Retrieve product list** | `GET /products` | `200 OK - List of products` |
| ✅ **Get order details** | `GET /order/12345` | `200 OK - Order details` |
| ✅ **Place a valid order** | `POST /order { "product_id": 101, "quantity": 2 }` | `201 Created - Order placed` |
| ❌ **Order with invalid quantity** | `POST /order { "quantity": -1 }` | `400 Bad Request - Invalid quantity` |
| ✅ **Update an order** | `PUT /order/12345 { "quantity": 3 }` | `200 OK - Order updated` |
| ❌ **Update a non-existing order** | `PUT /order/99999 { "quantity": 3 }` | `404 Not Found - Order not found` |
| ✅ **Cancel an existing order** | `DELETE /order/12345` | `200 OK - Order canceled` |
| ❌ **Cancel an already processed order** | `DELETE /order/67890` | `409 Conflict - Cannot cancel processed order` |
| ✅ **Make a payment** | `POST /payment { "order_id": 12345, "card_number": "****" }` | `200 OK - Payment successful` |
| ❌ **Payment with insufficient funds** | `POST /payment { "order_id": 12345, "card_number": "****" }` | `402 Payment Required - Payment declined` |

---

### **9️⃣ API Response Codes and Messages**
| **Status Code** | **Message** | **Meaning** |
|---------------|------------|------------|
| `200 OK` | Success | Request was successful. |
| `201 Created` | Order Created | New resource was successfully created. |
| `204 No Content` | Success, No Data | Request successful but no data to return. |
| `400 Bad Request` | Invalid Input | The request is invalid (e.g., negative quantity). |
| `401 Unauthorized` | Login Required | User is not logged in. |
| `403 Forbidden` | Access Denied | User does not have permission. |
| `404 Not Found` | Resource Not Found | The requested item or order does not exist. |
| `405 Method Not Allowed` | Invalid HTTP Method | The request used the wrong HTTP method (e.g., `PUT` instead of `POST`). |
| `409 Conflict` | Order Already Exists | Conflict occurred (e.g., duplicate order). |
| `500 Internal Server Error` | Server Error | An unexpected error occurred. |
| `502 Bad Gateway` | Payment Gateway Issue | Payment service is down. |

---

## **Conclusion**
- **Use `GET`** to **retrieve data** (e.g., product lists, order details).
- **Use `POST`** to **create new resources** (e.g., placing an order, making payments).
- **Use `PUT`** to **update existing resources** (e.g., modifying an order).
- **Use `DELETE`** to **remove resources** (e.g., canceling an order).
- **API Testing** validates backend communication.
- **Response Code Validation** ensures correct error handling.
